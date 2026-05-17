# CI/CD Pipelines

Continuous Integration and Continuous Delivery automate the path from code commit
to production deployment. CI/CD reduces manual effort, catches bugs early, and
enables teams to ship frequently with confidence.

---

## Definitions

| Term | Meaning |
|------|---------|
| **Continuous Integration (CI)** | Every commit is automatically built and tested |
| **Continuous Delivery (CD)** | Every passing build is automatically deployable to production |
| **Continuous Deployment** | Every passing build is automatically deployed to production (no human gate) |

Most organizations practice Continuous Delivery: the pipeline gets code to a
production-ready state, but a human approves the final deploy.

---

## Why CI/CD

**Without CI/CD**:
- "Big bang" merges — large diffs, hard to review, many conflicts
- Manual testing is slow and inconsistent
- Deploying is a stressful, high-risk event done infrequently

**With CI/CD**:
- Small changes integrate continuously — conflicts are small and caught early
- Every commit is automatically tested
- Deploying is routine and low-risk
- Bugs are caught in minutes, not days

---

## Pipeline Stages

```
Code Push
    │
    ▼
Source Stage
  ─ Checkout code
  ─ Restore dependency cache
    │
    ▼
Build Stage
  ─ Compile / transpile
  ─ Package (JAR, ZIP, Docker image)
    │
    ▼
Test Stage
  ─ Unit tests
  ─ Integration tests
  ─ Code coverage check
    │
    ▼
Security Scan
  ─ SAST (static analysis)
  ─ Dependency vulnerability scan
  ─ Secret scanning
  ─ Container image scan
    │
    ▼
Artifact
  ─ Push image to registry
  ─ Upload binary to artifact store
  ─ Tag with version / git SHA
    │
    ▼
Deploy (staging)
  ─ Deploy to staging environment
  ─ Run smoke tests / e2e tests
    │
    ▼
[Manual Approval Gate]
    │
    ▼
Deploy (production)
  ─ Canary or blue-green deploy
  ─ Monitor metrics for 10 minutes
  ─ Auto-rollback on error spike
    │
    ▼
Notify
  ─ Slack / PagerDuty on failure
  ─ PR status check update
```

---

## GitHub Actions

GitHub Actions is the most widely used CI/CD platform for teams on GitHub.

### Workflow File Structure

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]
  schedule:
    - cron: '0 2 * * *'          # Nightly at 2 AM UTC
  workflow_dispatch:               # Manual trigger

jobs:
  test:
    name: Test
    runs-on: ubuntu-latest         # GitHub-hosted runner
    strategy:
      matrix:
        node-version: [18, 20, 22]

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}
          cache: npm

      - name: Install dependencies
        run: npm ci

      - name: Run linter
        run: npm run lint

      - name: Run tests
        run: npm test -- --coverage

      - name: Upload coverage
        uses: codecov/codecov-action@v3
        with:
          token: ${{ secrets.CODECOV_TOKEN }}
```

### Triggers Reference

```yaml
on:
  push:
    branches: [main]
    paths:
      - 'src/**'           # Only trigger when src/ changes
      - 'package.json'
    paths-ignore:
      - '**.md'            # Ignore markdown changes

  pull_request:
    types: [opened, synchronize, reopened]

  workflow_call:           # Reusable workflow
    inputs:
      environment:
        type: string
        required: true
    secrets:
      deploy-key:
        required: true
```

### Secrets and Variables

```yaml
steps:
  - name: Deploy
    env:
      AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      APP_ENV: ${{ vars.APP_ENVIRONMENT }}    # vars = non-secret config
    run: |
      aws ecs update-service \
        --cluster prod \
        --service myapp \
        --force-new-deployment
```

```bash
# GITHUB_TOKEN: automatically provided, no setup needed
# Scoped to the repository; can push, create PRs, call APIs
```

### Caching

```yaml
- name: Cache node_modules
  uses: actions/cache@v3
  with:
    path: ~/.npm
    key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
    restore-keys: |
      ${{ runner.os }}-node-

- name: Cache Go modules
  uses: actions/cache@v3
  with:
    path: ~/go/pkg/mod
    key: ${{ runner.os }}-go-${{ hashFiles('**/go.sum') }}
```

### Artifacts

```yaml
- name: Build
  run: npm run build

- name: Upload build artifact
  uses: actions/upload-artifact@v3
  with:
    name: dist
    path: dist/
    retention-days: 5

# In another job:
- name: Download artifact
  uses: actions/download-artifact@v3
  with:
    name: dist
    path: dist/
```

### Full Node.js CI/CD Pipeline

```yaml
# .github/workflows/deploy.yml
name: CI/CD

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

env:
  ECR_REGISTRY: 123456789.dkr.ecr.us-east-1.amazonaws.com
  IMAGE_NAME: myapp
  AWS_REGION: us-east-1

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm
      - run: npm ci
      - run: npm test
      - run: npm run build

  security:
    runs-on: ubuntu-latest
    needs: test
    steps:
      - uses: actions/checkout@v4
      - name: Dependency scan
        run: npx audit-ci --moderate
      - name: Secret scan
        uses: trufflesecurity/trufflehog@main
        with:
          path: ./
          base: main

  build-and-push:
    runs-on: ubuntu-latest
    needs: [test, security]
    if: github.ref == 'refs/heads/main'
    outputs:
      image-tag: ${{ steps.meta.outputs.version }}
    steps:
      - uses: actions/checkout@v4

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ env.AWS_REGION }}

      - name: Login to ECR
        id: login-ecr
        uses: aws-actions/amazon-ecr-login@v2

      - name: Docker metadata
        id: meta
        uses: docker/metadata-action@v5
        with:
          images: ${{ env.ECR_REGISTRY }}/${{ env.IMAGE_NAME }}
          tags: |
            type=sha,prefix=sha-
            type=ref,event=branch

      - name: Build and push
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: ${{ steps.meta.outputs.tags }}
          cache-from: type=gha
          cache-to: type=gha,mode=max

      - name: Scan image
        uses: aquasecurity/trivy-action@master
        with:
          image-ref: ${{ env.ECR_REGISTRY }}/${{ env.IMAGE_NAME }}:sha-${{ github.sha }}
          exit-code: 1
          severity: CRITICAL,HIGH

  deploy-staging:
    runs-on: ubuntu-latest
    needs: build-and-push
    environment: staging
    steps:
      - name: Configure AWS
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ env.AWS_REGION }}
      - name: Deploy to staging ECS
        run: |
          aws ecs update-service \
            --cluster staging \
            --service myapp \
            --force-new-deployment

  deploy-prod:
    runs-on: ubuntu-latest
    needs: deploy-staging
    environment:
      name: production          # Requires manual approval in GitHub
      url: https://myapp.com
    steps:
      - name: Configure AWS
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ env.AWS_REGION }}
      - name: Deploy to production ECS
        run: |
          aws ecs update-service \
            --cluster production \
            --service myapp \
            --force-new-deployment
```

---

## GitLab CI/CD

```yaml
# .gitlab-ci.yml
stages:
  - test
  - build
  - deploy

variables:
  DOCKER_IMAGE: $CI_REGISTRY_IMAGE:$CI_COMMIT_SHA

test:
  stage: test
  image: node:20-alpine
  cache:
    key: $CI_COMMIT_REF_SLUG
    paths:
      - node_modules/
  script:
    - npm ci
    - npm test
  coverage: '/All files[^|]*\|[^|]*\s+([\d\.]+)/'
  artifacts:
    reports:
      coverage_report:
        coverage_format: cobertura
        path: coverage/cobertura-coverage.xml

build:
  stage: build
  image: docker:24
  services:
    - docker:dind
  before_script:
    - docker login -u $CI_REGISTRY_USER -p $CI_REGISTRY_PASSWORD $CI_REGISTRY
  script:
    - docker build -t $DOCKER_IMAGE .
    - docker push $DOCKER_IMAGE
  only:
    - main

deploy:staging:
  stage: deploy
  environment:
    name: staging
    url: https://staging.example.com
  script:
    - kubectl set image deployment/myapp app=$DOCKER_IMAGE
  only:
    - main

deploy:production:
  stage: deploy
  environment:
    name: production
    url: https://example.com
  when: manual           # Requires human click
  script:
    - kubectl set image deployment/myapp app=$DOCKER_IMAGE -n production
  only:
    - main
```

---

## Deployment Strategies

### Rolling Update

Replace instances one at a time. Old and new versions run simultaneously briefly.

```yaml
# Kubernetes Deployment rolling update
spec:
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 25%           # Extra pods allowed during update
      maxUnavailable: 25%     # Pods allowed to be down during update
```

**Pros**: No extra infrastructure. Simple.
**Cons**: Brief period of mixed versions; rollback requires another rolling update.

### Blue-Green

Maintain two identical environments. Switch traffic from blue (current) to green (new) instantly.

```
Users → Load Balancer → [Blue] (v1.0) ← current
                      → [Green] (v1.1) ← test here, then flip
```

**Pros**: Zero-downtime, instant rollback (just flip back).
**Cons**: Requires 2x infrastructure cost during deploy.

### Canary

Route a small percentage of traffic to the new version. Gradually increase.

```
100% → v1.0

After deploy:
 95% → v1.0
  5% → v1.1    ← monitor error rates, latency

After validation:
100% → v1.1
```

**Pros**: Limits blast radius; catches issues with real traffic.
**Cons**: Need traffic splitting capability (ALB weighted target groups, Istio, etc.).

---

## GitOps with ArgoCD

GitOps: the Git repository is the single source of truth for the desired state
of the infrastructure. ArgoCD watches Git and applies changes to Kubernetes.

```yaml
# ArgoCD Application
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: myapp
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/org/gitops-repo
    targetRevision: main
    path: k8s/overlays/production
  destination:
    server: https://kubernetes.default.svc
    namespace: production
  syncPolicy:
    automated:
      prune: true       # Delete resources removed from Git
      selfHeal: true    # Revert manual changes in cluster
    syncOptions:
      - CreateNamespace=true
```

---

## DORA Metrics

DORA (DevOps Research and Assessment) identifies four metrics that predict software
delivery performance and organizational performance:

| Metric | Elite | High | Medium | Low |
|--------|-------|------|--------|-----|
| **Deployment Frequency** | Multiple/day | Weekly | Monthly | Bi-annually |
| **Lead Time for Changes** | < 1 hour | 1 day–1 week | 1–6 months | > 6 months |
| **Change Failure Rate** | 0–15% | 0–15% | 16–30% | 16–30% |
| **MTTR** | < 1 hour | < 1 day | 1–6 months | > 6 months |

These metrics are the output of good CI/CD practices, not goals to game.
