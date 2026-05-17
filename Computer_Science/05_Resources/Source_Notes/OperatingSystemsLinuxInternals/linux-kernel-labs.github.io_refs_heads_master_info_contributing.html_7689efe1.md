Title: Contributing to linux-kernel-labs — The Linux Kernel  documentation
Mapped Topic: Kernel labs and lectures
Source URL: https://linux-kernel-labs.github.io/refs/heads/master/info/contributing.html
Source Type: official_course_material
Trust Score: 95
Fetched At: 2026-04-17T07:05:59+00:00
Mapped From CSE.md Section: Part 2: C. Operating systems, Linux internals, kernel understanding

# Content

# Contributing to linux-kernel-labs[¶](https://linux-kernel-labs.github.io#contributing-to-linux-kernel-labs)

`linux-kernel-labs`

is an open platform.
You can help it get better by contributing to the documentation, exercises or
the infrastructure.
All contributions are welcome, no matter if they are just fixes for typos or
new sections in the documentation.

All information required for making a contribution can be found in the
[linux-kernel-labs Linux repo](https://github.com/linux-kernel-labs/linux).
In order to change anything, you need to create a Pull Request (`PR`

)
from your own fork to this repository.
The PR will be reviewed by the members of the team and will be merged once
any potential issue is fixed.

## Repository structure[¶](https://linux-kernel-labs.github.io#repository-structure)

The [linux-kernel-labs repo](https://github.com/linux-kernel-labs/linux) is
a fork of the Linux kernel repo, with the following additions:

`/tools/labs`

: contains the labs and the[virtual machine (VM) infrastructure]

`tools/labs/templates`

: contains the skeletons sources`tools/labs/qemu`

: contains the qemu VM configuration`/Documentation/teaching`

: contains the sources used to generate this documentation

## Building the documentation[¶](https://linux-kernel-labs.github.io#building-the-documentation)

To build the documentation, navigate to `tools/labs`

and run the following
command:

```
make docs
```

Note

The command should install all the required packages. In some cases, installing the packages or building the documentation might fail, because of broken dependencies versions.

Instead of struggling to fix the dependencies, the simplest way to build
the documentation is using a [Docker](https://www.docker.com/).
First, install `docker`

and `docker-compose`

on your host, and then run:

```
make docker-docs
```

The first run might take some time, but subsequent builds will be faster.

## Creating a contribution[¶](https://linux-kernel-labs.github.io#creating-a-contribution)

### Forking the repository[¶](https://linux-kernel-labs.github.io#forking-the-repository)

If you haven't done it already, clone the

[linux-kernel-labs repo](https://github.com/linux-kernel-labs/linux)repository locally:$ mkdir -p ~/src $ git clone git@github.com:linux-kernel-labs/linux.git ~/src/linux

Go to

[https://github.com/linux-kernel-labs/linux](https://github.com/linux-kernel-labs/linux), make sure you are logged in and click`Fork`

in the top right of the page.Add the forked repo as a new remote to the local repo:

$ git remote add my_fork git@github.com:<your_username>/linux.git

Now, you can push to your fork by using `my_fork`

instead of `origin`

(e.g. `git push my_fork master`

).

### Creating a pull request[¶](https://linux-kernel-labs.github.io#creating-a-pull-request)

Warning

Pull requests must be created from their own branches, which are started from
`master`

.

- Go to the master branch and make sure you have no local changes:

`student@eg106:~/src/linux$ git checkout master student@eg106:~/src/linux$ git status On branch master Your branch is up-to-date with 'origin/master'. nothing to commit, working directory clean`

- Make sure the local master branch is up-to-date with linux-kernel-labs:

student@eg106:~/src/linux$ git pull origin masterNote

You can also push the latest master to your forked repo:

student@eg106:~/src/linux$ git push my_fork master

- Create a new branch for your change:

student@eg106:~/src/linux$ git checkout -b <your_branch_name>

- Make some changes and commit them. In this example, we are going to change
`Documentation/teaching/index.rst`

:

`student@eg106:~/src/linux$ vim Documentation/teaching/index.rst student@eg106:~/src/linux$ git add Documentation/teaching/index.rst student@eg106:~/src/linux$ git commit -m "<commit message>"`

Warning

The commit message must include a relevant description of your change and the location of the changed component.

Examples:

`documentation: index: Fix typo in the first section`

`labs: block_devices: Change printk log level`

- Push the local branch to your forked repository:

student@eg106:~/src/linux$ git push my_fork <your_branch_name>

- Open the Pull Request

- Go to
[https://github.com]and open your forked repository page- Click
`New pull request`

.- Make sure base repository (left side) is
`linux-kernel-labs/linux`

and the base is master.- Make sure the head repository (right side) is your forked repo and the compare branch is your pushed branch.
- Click
`Create pull request`

.

### Making changes to a Pull Request[¶](https://linux-kernel-labs.github.io#making-changes-to-a-pull-request)

After receiving feedback for your changes, you might need to update the Pull Request. Your goal is to do a new push on the same branch. For this, follow the next steps:

- Make sure your branch is still up to date with the
`linux-kernel-labs`

repo`master`

branch.

student@eg106:~/src/linux$ git fetch origin master student@eg106:~/src/linux$ git rebase FETCH_HEADNote

If you are getting conflicts, it means that someone else modified the same files/lines as you and already merged the changes since you opened the Pull Request.

In this case, you will need to fix the conflicts by editing the conflicting files manually (run

`git status`

to see these files). After fixing the conflicts, add them using`git add`

and then run`git rebase --continue`

.

- Apply the changes to your local files
- Commit the changes. We want all the changes to be in the same commit, so we will amend the changes to the initial commit.

student@eg106:~/src/linux$ git add Documentation/teaching/index.rst student@eg106:~/src/linux$ git commit --amend

- Force-push the updated commit:

student@eg106:~/src/linux$ git push my_fork <your_branch_name> -fAfter this step, the Pull Request is updated. It is now up to the linux-kernel-labs team to review the pull request and integrate your contributions in the main project.
