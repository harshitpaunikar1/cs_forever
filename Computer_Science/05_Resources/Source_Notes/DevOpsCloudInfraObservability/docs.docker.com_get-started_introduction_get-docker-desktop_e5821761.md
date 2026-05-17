Title: Get Docker Desktop | Docker Docs
Mapped Topic: Containers and images
Source URL: https://docs.docker.com/get-started/introduction/get-docker-desktop/
Source Type: official_docs
Trust Score: 97
Fetched At: 2026-04-17T07:10:46+00:00
Mapped From CSE.md Section: Part 2: G. DevOps / cloud / infra / observability

# Content

# Get Docker Desktop

[Explanation](https://docs.docker.com#explanation)

Docker Desktop is the all-in-one package to build images, run containers, and so much more. This guide will walk you through the installation process, enabling you to experience Docker Desktop firsthand.

Docker Desktop termsCommercial use of Docker Desktop in larger enterprises (more than 250 employees OR more than $10 million USD in annual revenue) requires a

[paid subscription].

### Docker Desktop for Mac

### Docker Desktop for Windows

### Docker Desktop for Linux

Once it's installed, complete the setup process and you're all set to run a Docker container.

[Try it out](https://docs.docker.com#try-it-out)

In this hands-on guide, you will see how to run a Docker container using Docker Desktop.

Follow the instructions to run a container using the CLI.

[Run your first container](https://docs.docker.com#run-your-first-container)

Open your CLI terminal and start a container by running the `docker run`

command:

```
$ docker run -d -p 8080:80 docker/welcome-to-docker
```

[Access the frontend](https://docs.docker.com#access-the-frontend)

For this container, the frontend is accessible on port `8080`

. To open the website, visit [http://localhost:8080](http://localhost:8080) in your browser.

[Manage containers using Docker Desktop](https://docs.docker.com#manage-containers-using-docker-desktop)

Open Docker Desktop and select the

**Containers**field on the left sidebar.You can view information about your container including logs, and files, and even access the shell by selecting the

**Exec**tab.Select the

**Inspect**field to obtain detailed information about the container. You can perform various actions such as pause, resume, start or stop containers, or explore the**Logs**,**Bind mounts**,**Exec**,**Files**, and**Stats**tabs.

Docker Desktop simplifies container management for developers by streamlining the setup, configuration, and compatibility of applications across different environments, thereby addressing the pain points of environment inconsistencies and deployment challenges.

[What's next?](https://docs.docker.com#whats-next)

Now that you have Docker Desktop installed and ran your first container, it's time to start developing with containers.

[Develop with containers](https://docs.docker.com/get-started/introduction/develop-with-containers/)
