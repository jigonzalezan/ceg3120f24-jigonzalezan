# ceg3120f24-jigonzalezan
# Basics Guide - CEG3120

A personal reference guide for Git, Docker, and SSH commands and concepts used in this course.

---

## 1. Command Line Git

* **status**: Shows status of the local repository. This includes: number of local commits that have not been synced with remote (GitHub), list of files in local folder that are NOT being tracked by git, and list of files in local folder that have changes that need to be committed.
  * *Example*: `git status`
* **log**: Displays the commit history for the current branch.
  * *Example*: `git log`
* **clone**: Creates a local working copy of an existing remote repository.
  * *Example*: `git clone https://github.com/jigonzalezan/ceg3120f24-jigonzalezan.git`
* **remote**: Manages tracked remote repositories (view, add, or remove remote connections).
  * *Example*: `git remote -v`
* **add**: Adds file changes from the working directory to the staging area.
  * *Example*: `git add basics-guide/README.md`
* **rm**: Removes files from the working tree and index.
  * *Remove from tracking only (keep local file on disk)*: `git rm --cached filename.txt`
  * *Fully remove from tracking AND working directory*: `git rm filename.txt`
* **commit**: Captures a snapshot of the staged changes with a descriptive log message.
  * *Example*: `git commit -m "docs: add git commands section"`
* **push**: Uploads local branch commits to the remote repository.
  * *Example*: `git push origin main`
* **pull**: Fetches updates from a remote repository and merges them into the current active branch.
  * *Example*: `git pull origin main`
* **branch**: Lists, creates, or deletes local branches.
  * *Example*: `git branch dev`
* **checkout**: Switches branches or restores working tree files.
  * *Example*: `git checkout dev`
* **fetch**: Downloads objects and refs from another repository without merging changes into local branches.
  * *Example*: `git fetch origin`
* **merge**: Combines the specified branch's history into the current active branch.
  * *Example*: `git merge dev`
* **init**: Initializes a new Git repository.
  * *Initialize an existing local directory*: `git init`
  * *Create a bare repository (stores version history only, no working directory)*: `git init --bare project.git`

---

## 2. Git Files & Folders

### `.git` Folder
The `.git` folder is a hidden directory at the root of a Git repository that contains all tracking data, metadata, and configuration for version control.
* **HEAD**: Pointer file indicating the currently checked-out branch or commit.
* **config**: Repository-specific settings, including remote URLs and branch rules.
* **hooks/**: Scripts that run automatically before or after Git events (e.g., pre-commit, post-merge).
* **index**: Binary file holding staging area information before commits are made.
* **objects/**: Database containing all blob contents, tree structures, and commit objects.
* **refs/**: References pointing to specific commit objects (branches in `heads/`, tags, and remote tracking branches).

### `.gitignore` File
* **Location**: Located in the root directory of the repository (`/.gitignore`).
* **Purpose**: Specifies intentionally untracked files and folder patterns (e.g., OS clutter, credentials, logs) that Git should ignore to prevent accidental tracking.

---

## 3. Command Line Docker

* **ps**: Lists containers.
  * *View active (running) containers*: `docker ps`
  * *View all containers (active, stopped, exited)*: `docker ps -a`
* **images**: Lists all locally available Docker images with tags and sizes.
  * *Example*: `docker images`
* **run**: Creates and starts a new container from an image.
  * *Example*: `docker run -it -p 8080:80 --name my-web-server nginx`
  * *Flags*: `-it` runs interactively with a pseudo-TTY terminal; `-p` maps host port to container port (`host:container`); `--name` assigns a custom container name.
* **start**: Starts one or more stopped containers.
  * *Example*: `docker start my-web-server`
* **stop**: Gracefully stops a running container.
  * *Example*: `docker stop my-web-server`
* **exec**: Runs a command inside a currently running container.
  * *Example*: `docker exec -it my-web-server bash`
* **import**: Creates a filesystem image from a tarball archive.
  * *Example*: `docker import archive.tar my-image:latest`
* **export**: Exports a container's filesystem as a tar archive.
  * *Example*: `docker export my-web-server -o container.tar`
* **kill**: Forcefully shuts down a running container immediately (`SIGKILL`).
  * *Example*: `docker kill my-web-server`
* **rm**: Removes containers or images.
  * *Remove container*: `docker rm my-web-server`
  * *Remove image*: `docker rmi nginx`

---

## 4. SSH Guides

### Setting up SSH Authentication to GitHub Repositories
1. **Create SSH Key Pair**: Run `ssh-keygen -t ed25519 -C "your_email@example.com"` in terminal and follow prompts.
2. **Setup Public Key on GitHub**: Copy public key (`cat ~/.ssh/id_ed25519.pub`), navigate to **GitHub Settings > SSH and GPG keys > New SSH Key**, and paste it.
3. **Get SSH URI for Cloning**: Go to the repository page, click **Code**, select the **SSH** tab, and copy the URI (e.g., `git@github.com:jigonzalezan/ceg3120f24-jigonzalezan.git`).
4. **Clone via SSH**: Run `git clone git@github.com:jigonzalezan/ceg3120f24-jigonzalezan.git`.

### Setting up SSH Authentication and Connecting to an AWS Instance
1. **Retrieve Private Key**: Download the `.pem` key file generated during AWS EC2 instance creation.
2. **Set Private Key Permissions**: Restrict permissions so only the owner can read it: `chmod 400 /path/to/key.pem`.
3. **Find Public IP**: Go to **AWS Management Console > EC2 > Instances** and copy the **Public IPv4 address**.
4. **Establish Connection**: Run `ssh -i "/path/to/key.pem" ubuntu@<PUBLIC_IP>`.

### Using the Config File in the `.ssh` Folder
1. Open or create `~/.ssh/config` and add an entry block:


text
Host aws-server
HostName 54.210.10.1
User ubuntu
IdentityFile ~/.ssh/my-aws-key.pem


2. **Connect using configured alias**: Run `ssh aws-server`.

---

## 5. Resources

* [Git Documentation](https://git-scm.com/doc) - Used for official Git command explanations and definitions.
* [Docker Documentation](https://docs.docker.com/engine/reference/commandline/cli/) - Used for Docker command usage and flag specifications.
* [GitHub SSH Setup Guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) - Reference for SSH key generation and GitHub authentication.
* [AWS EC2 Connecting Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html) - Reference for connecting to Linux EC2 instances.
