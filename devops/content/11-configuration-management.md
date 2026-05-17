# Configuration Management

Configuration management tools keep servers and their software in a declared
desired state. They apply configurations idempotently — running the same
playbook/manifest twice produces the same result. This page focuses on Ansible
(the most common DevOps choice) with comparisons to Chef, Puppet, and SaltStack.

---

## What Configuration Management Solves

| Without CM | With CM |
|------------|---------|
| SSH into each server to make changes | Run one command against 1000 servers |
| "Snowflake servers" — each one slightly different | All servers identical, defined in code |
| No audit trail of what changed | Every change is in version control |
| Manual, error-prone application | Idempotent, automated |
| Onboarding a new server takes hours | Minutes: run the playbook |

---

## Push vs Pull

**Push model** (Ansible): the control machine connects to target nodes and pushes changes.
- Simpler: no agent on target nodes
- Immediate: changes apply when you run the command
- Requires SSH/WinRM connectivity from control to targets

**Pull model** (Chef, Puppet, Salt): agents on target nodes periodically pull configuration from a central server.
- Scales better for large fleets
- Self-healing: drift is corrected automatically on schedule
- Requires running agents on every node

---

## Ansible

Ansible uses SSH to connect to target machines and execute modules.
No agent needed on managed nodes — just Python (which most Linux systems have).

### Architecture

```
Control Node (your laptop or CI runner)
  └── Inventory (list of target hosts)
  └── Playbooks (YAML: what to do)
  └── Roles (reusable playbook components)
  └── ansible.cfg (configuration)
          │ SSH
          ▼
Managed Nodes (your servers)
  └── /tmp/ansible-<random>/   ← Ansible copies modules here, executes, cleans up
```

### Installation

```bash
pip install ansible
pip install ansible boto3 botocore  # For AWS dynamic inventory

ansible --version
ansible-galaxy collection install community.general
ansible-galaxy collection install amazon.aws
```

### Configuration: ansible.cfg

```ini
[defaults]
inventory       = ./inventory
remote_user     = ubuntu
private_key_file = ~/.ssh/id_ed25519
host_key_checking = False           # Don't prompt for new host keys
stdout_callback = yaml              # Nicer output
retry_files_enabled = False

[privilege_escalation]
become = True
become_method = sudo
become_user = root
```

---

### Inventory

**Static inventory (INI format)**:

```ini
# inventory/hosts
[webservers]
web1.example.com
web2.example.com ansible_host=10.0.0.5  # Override connection IP

[databases]
db1.example.com
db2.example.com

[production:children]  # Group of groups
webservers
databases

[webservers:vars]      # Variables for group
http_port=80
nginx_version=1.25

[all:vars]
ansible_user=ubuntu
ansible_python_interpreter=/usr/bin/python3
```

**Static inventory (YAML format)**:

```yaml
# inventory/hosts.yml
all:
  children:
    webservers:
      hosts:
        web1.example.com:
        web2.example.com:
          ansible_host: 10.0.0.5
      vars:
        http_port: 80
    databases:
      hosts:
        db1.example.com:
```

**Dynamic inventory (AWS)**:

```bash
# Use the AWS dynamic inventory plugin
ansible-inventory --list -i aws_ec2.yml

# aws_ec2.yml
plugin: amazon.aws.aws_ec2
regions:
  - us-east-1
filters:
  tag:Environment: production
keyed_groups:
  - key: tags.Role
    prefix: role
hostnames:
  - private-dns-name
```

---

### Ad-hoc Commands

```bash
# Ping all hosts
ansible all -m ping

# Run a command
ansible webservers -m command -a "uptime"

# Run a shell command (with pipes, etc.)
ansible webservers -m shell -a "df -h | grep /dev"

# Copy a file
ansible webservers -m copy -a "src=./nginx.conf dest=/etc/nginx/nginx.conf"

# Install a package
ansible webservers -m apt -a "name=nginx state=present" --become

# Restart a service
ansible webservers -m service -a "name=nginx state=restarted" --become

# Gather facts about a host
ansible web1.example.com -m setup
ansible web1.example.com -m setup -a "filter=ansible_distribution*"

# Run with specific inventory file
ansible -i inventory/prod/hosts webservers -m ping

# Limit to specific hosts
ansible webservers -m ping --limit web1.example.com
ansible webservers -m ping --limit "web1,web2"
```

---

### Playbooks

```yaml
# playbooks/configure-webserver.yml
---
- name: Configure web servers
  hosts: webservers
  become: true
  gather_facts: true

  vars:
    nginx_port: 80
    app_dir: /opt/app

  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes
        cache_valid_time: 3600  # Only update if cache is > 1 hour old

    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Create app directory
      file:
        path: "{{ app_dir }}"
        state: directory
        owner: www-data
        group: www-data
        mode: '0755'

    - name: Deploy Nginx config
      template:
        src: templates/nginx.conf.j2
        dest: /etc/nginx/nginx.conf
        owner: root
        group: root
        mode: '0644'
        validate: nginx -t -c %s   # Validate before placing
      notify: Reload Nginx          # Trigger handler

    - name: Ensure Nginx is started and enabled
      service:
        name: nginx
        state: started
        enabled: yes

    - name: Open firewall port
      ufw:
        rule: allow
        port: "{{ nginx_port }}"
        proto: tcp

  handlers:
    - name: Reload Nginx
      service:
        name: nginx
        state: reloaded
```

**Key directives**:

| Directive | Purpose |
|-----------|---------|
| `hosts` | Target hosts or groups |
| `become` | Run tasks as sudo |
| `gather_facts` | Collect host info before tasks |
| `vars` | Play-level variables |
| `tasks` | List of tasks to execute |
| `handlers` | Tasks triggered by `notify` |
| `when` | Conditional execution |
| `loop` | Iterate over a list |
| `register` | Store task output in a variable |
| `notify` | Trigger a handler |
| `tags` | Label tasks for selective running |

### Conditionals and Loops

```yaml
tasks:
  - name: Install package (RedHat)
    yum:
      name: nginx
      state: present
    when: ansible_os_family == "RedHat"

  - name: Install package (Debian)
    apt:
      name: nginx
      state: present
    when: ansible_os_family == "Debian"

  - name: Install multiple packages
    apt:
      name: "{{ item }}"
      state: present
    loop:
      - nginx
      - curl
      - git
      - htop

  - name: Create users
    user:
      name: "{{ item.name }}"
      groups: "{{ item.groups }}"
      state: present
    loop:
      - { name: alice, groups: sudo }
      - { name: bob,   groups: docker }

  - name: Run a command and check result
    command: systemctl is-active nginx
    register: nginx_status
    changed_when: false   # Don't mark as changed

  - name: Print nginx status
    debug:
      msg: "Nginx is {{ nginx_status.stdout }}"
```

### Variables and Precedence

Ansible has 22 variable precedence levels. Most important (low to high):

1. Role defaults (`roles/nginx/defaults/main.yml`)
2. Inventory group vars (`group_vars/all.yml`)
3. Inventory host vars (`host_vars/web1.yml`)
4. Play vars (`vars:` in playbook)
5. Task vars (`vars:` in task)
6. Extra vars from command line (`-e`) ← **highest priority**

```yaml
# group_vars/webservers.yml
nginx_worker_processes: auto
nginx_worker_connections: 1024

# host_vars/web1.example.com.yml
nginx_worker_connections: 2048   # Override for this host
```

---

### Ansible Vault

Encrypt sensitive data:

```bash
# Encrypt a file
ansible-vault encrypt secrets.yml

# Create an encrypted file
ansible-vault create vars/vault.yml

# Edit encrypted file
ansible-vault edit vars/vault.yml

# View encrypted file
ansible-vault view vars/vault.yml

# Decrypt
ansible-vault decrypt vars/vault.yml

# Run playbook with vault password
ansible-playbook site.yml --ask-vault-pass
ansible-playbook site.yml --vault-password-file ~/.vault_pass

# Inline encrypted variable
ansible-vault encrypt_string 'mypassword' --name 'db_password'
```

```yaml
# vars/vault.yml (encrypted at rest)
vault_db_password: "supersecret"
vault_api_key: "abc123"

# vars/main.yml (plain text, references vault vars)
db_password: "{{ vault_db_password }}"
```

---

### Jinja2 Templates

```jinja2
{# templates/nginx.conf.j2 #}
worker_processes {{ nginx_worker_processes }};
worker_connections {{ nginx_worker_connections }};

http {
    server {
        listen {{ nginx_port }};
        server_name {{ ansible_fqdn }};

        {% if enable_ssl %}
        listen 443 ssl;
        ssl_certificate {{ ssl_cert_path }};
        {% endif %}

        {% for location in nginx_locations %}
        location {{ location.path }} {
            proxy_pass http://{{ location.upstream }};
        }
        {% endfor %}
    }
}
```

---

### Roles

Roles are reusable, self-contained components with a standard directory structure:

```
roles/
└── nginx/
    ├── defaults/
    │   └── main.yml       # Default variable values
    ├── files/
    │   └── mime.types     # Static files
    ├── handlers/
    │   └── main.yml       # Handlers
    ├── meta/
    │   └── main.yml       # Role metadata and dependencies
    ├── tasks/
    │   └── main.yml       # Main task list
    ├── templates/
    │   └── nginx.conf.j2  # Jinja2 templates
    └── vars/
        └── main.yml       # Role variables (higher precedence than defaults)
```

```yaml
# Using roles in a playbook
- hosts: webservers
  roles:
    - role: nginx
      vars:
        nginx_port: 8080

# Install roles from Ansible Galaxy
ansible-galaxy install geerlingguy.nginx
ansible-galaxy install -r requirements.yml
```

```yaml
# requirements.yml
roles:
  - name: geerlingguy.nginx
    version: 3.1.0
  - src: https://github.com/org/ansible-role-myapp
    name: myapp

collections:
  - name: community.general
    version: ">=7.0.0"
```

---

### Error Handling

```yaml
tasks:
  - name: Try to start service
    service:
      name: myservice
      state: started
    ignore_errors: yes      # Continue even if this fails

  - name: Run script that may fail
    command: /opt/deploy.sh
    failed_when: false      # Never mark as failed

  - name: Custom failure condition
    command: check_status.sh
    register: result
    failed_when: result.rc != 0 and result.rc != 2

  - name: Block with rescue
    block:
      - name: Try to deploy
        command: deploy.sh
      - name: Run migrations
        command: migrate.sh
    rescue:
      - name: Rollback on failure
        command: rollback.sh
    always:
      - name: Send notification
        slack:
          msg: "Deploy {{ 'succeeded' if ansible_failed_task is not defined else 'failed' }}"
```

---

## Chef vs Puppet vs SaltStack (Brief)

### Chef

- Configuration defined in **Ruby DSL** (cookbooks → recipes → resources)
- Push or pull model
- Chef Workstation → Chef Server → nodes (agent: `chef-client`)
- Strong ecosystem, complex learning curve

```ruby
# Recipe example
package 'nginx'
service 'nginx' do
  action [:enable, :start]
end
template '/etc/nginx/nginx.conf' do
  source 'nginx.conf.erb'
  notifies :reload, 'service[nginx]'
end
```

### Puppet

- Declarative DSL or Ruby
- Pull model: agents run `puppet agent -t` on schedule or via orchestration
- Puppet Server → nodes (agent: `puppet agent`)
- Strong compliance and reporting; widely used in large enterprises

```puppet
# Manifest example
package { 'nginx':
  ensure => installed,
}
service { 'nginx':
  ensure  => running,
  enable  => true,
  require => Package['nginx'],
}
```

### SaltStack

- Python-based; fast (ZeroMQ messaging between master and minions)
- Push (salt master → minions) or pull
- YAML states with Jinja2; powerful event-driven orchestration
- Grains (facts about minions), Pillars (sensitive data for minions)

```bash
salt '*' test.ping
salt 'web*' state.apply nginx
salt-call state.apply    # Run on a minion locally
```

---

## Comparison Table

| | Ansible | Chef | Puppet | SaltStack |
|--|---------|------|--------|-----------|
| **Language** | YAML | Ruby | Puppet DSL | YAML/Python |
| **Model** | Push | Push/Pull | Pull | Push/Pull |
| **Agent** | Agentless | Required | Required | Required |
| **Learning curve** | Low | High | Medium | Medium |
| **Performance at scale** | Slower (SSH) | Fast | Moderate | Very fast |
| **Windows support** | Good (WinRM) | Good | Good | Limited |
| **K8s world** | Helm/kubectl | Mostly replaced | Mostly replaced | Limited |

---

## Configuration Management in a Kubernetes World

In Kubernetes environments, much of configuration management moves to:

- **Helm**: package manager for Kubernetes; charts are parameterized templates
- **Kustomize**: overlay-based configuration for Kubernetes manifests
- **GitOps (ArgoCD, Flux)**: declarative, Git-driven cluster configuration
- **Ansible** is still used for:
  - Provisioning the nodes that run Kubernetes
  - Bootstrapping cluster tooling
  - Managing non-containerized services
