# Basics Guide - CEG3120

A comprehensive personal reference guide for Git, Docker, and SSH operations used throughout this course.

---

## 1. Command Line Git

* **status**: Shows status of the local repository. This includes the number of local commits that have not been synced with the remote, a list of untracked files, and tracked files with modified changes.
  * *Example*: `git status`
* **log**: Displays the commit history for the current active branch.
  * *Example*: `git log`
* **clone**: Downloads an existing remote repository into a new local working directory.
  * *Example*: `git clone https://github.com/jigonzalezan/ceg3120f24-jigonzalezan.git`
* **remote**: Manages tracked remote repositories (view, add, or remove remote connections).
  * *Example*: `git remote -v`
* **add**: Adds file changes from the working directory to the staging area (index) for the next commit.
  * *Example*: `git add basics-guide/README.md`
* **rm**: Removes files from the working tree and index.
  * *Remove from tracking only (keep local file on disk)*: `git rm --cached filename.txt`
  * *Fully remove from tracking AND working directory*: `git rm filename.txt`
* **commit**: Captures a snapshot of the staged changes with a descriptive log message.
  * *Example*: `git commit -m "docs: add git commands section"`
* **push**: Uploads local branch commits to the remote repository branch.
  * *Example*: `git push origin dev`
* **pull**: Fetches updates from a remote repository branch and immediately merges them into the current active branch.
  * *Example*: `git pull origin main`
* **branch**: Lists, creates, or deletes local branches.
  * *Example*: `git branch dev`
* **checkout**: Switches branches or restores working tree files.
  * *Example*: `git checkout dev`
* **fetch**: Downloads objects and refs from another repository without merging changes into local branches.
  * *Example*: `git fetch origin`
* **merge**: Integrates changes from a specified branch into the current active branch.
  * *Example*: `git merge dev`
* **init**: Initializes a new Git repository.
  * *Initialize an existing local directory (non-bare)*: `git init`
  * *Create a bare repository (stores version history and objects only, with no working directory)*: `git init --bare project.git`

---

## 2. Git Files & Folders

### `.git` Folder
The `.git` folder is a hidden directory at the root of a Git repository that stores all tracking data, metadata, and object history for version control.
* **HEAD**: Reference file pointing to the currently checked-out branch or commit.
* **config**: Repository-specific settings file holding remote URLs, user details, and branch configurations.
* **hooks/**: Directory containing client-side or server-side scripts that run automatically on Git events (e.g., pre-commit, post-merge).
* **index**: Binary staging file acting as a cache between the working directory and repository history.
* **objects/**: Database storing all repository content as content-addressable objects (blobs, trees, commits, tags).
* **refs/**: References pointing to specific commit objects (local branches under `heads/`, remote tracking branches under `remotes/`, and `tags/`).

### `.gitignore` File
* **Location**: Located in the root directory of the repository (`/.gitignore`).
* **Purpose**: Specifies intentionally untracked file patterns (such as build outputs, secret environment files, or OS system files) that Git should ignore and never prompt to stage.

---

## 3. Command Line Docker

* **ps**: Lists containers.
  * *View active (running) containers*: `docker ps`
  * *View all containers (active, stopped, exited)*: `docker ps -a`
* **images**: Displays all locally downloaded Docker images with their tags and sizes.
  * *Example*: `docker images`
* **run**: Creates and starts a new container instance from a specified image.
  * *Example*: `docker run -it -p 8080:80 --name my-web-server nginx`
  * *Flags*: `-it` runs interactively with a pseudo-TTY terminal; `-p` maps host port to container port (`host:container`); `--name` assigns a custom container name.
* **start**: Starts one or more stopped containers.
  * *Example*: `docker start my-web-server`
* **stop**: Gracefully stops one or more running containers.
  * *Example*: `docker stop my-web-server`
* **exec**: Executes a new command inside a running container.
  * *Example*: `docker exec -it my-web-server bash`
* **import**: Creates a container filesystem image from a specified tarball archive.
  * *Example*: `docker import rootfs.tar my-custom-image:latest`
* **export**: Exports a container's filesystem as a tar archive.
  * *Example*: `docker export my-web-server -o container_backup.tar`
* **kill**: Forcefully shuts down a running container immediately (`SIGKILL`).
  * *Example*: `docker kill my-web-server`
* **rm**: Removes containers or images from local storage.
  * *Removing a container*: `docker rm my-web-server`
  * *Removing an image*: `docker rmi nginx`

---

## 4. SSH Guides

### Setting up SSH Authentication to GitHub Repositories
1. **Create SSH Key Pair**: Open terminal and run `ssh-keygen -t ed25519 -C "your_email@example.com"`, then follow the prompts.
2. **Setup Public Key on GitHub**: Copy the public key output (`cat ~/.ssh/id_ed25519.pub`), then go to **GitHub > Settings > SSH and GPG keys > New SSH Key** and paste it.
3. **Get SSH URI for Cloning**: Navigate to your repository on GitHub, click the green **Code** button, select the **SSH** tab, and copy the URI (e.g., `git@github.com:jigonzalezan/ceg3120f24-jigonzalezan.git`).
4. **Clone via SSH**: Run `git clone git@github.com:jigonzalezan/ceg3120f24-jigonzalezan.git`.

### Setting up SSH Authentication and Connecting to an AWS Instance
1. **Retrieve Private Key**: Download the `.pem` private key file provided during AWS EC2 instance creation.
2. **Set Private Key Permissions**: Protect the key file by setting read-only permissions: `chmod 400 /path/to/your-key.pem`.
3. **Find Public IP**: Locate the Public IPv4 Address under **AWS Console > EC2 > Instances > Instance Details**.
4. **Establish SSH Connection**: Run `ssh -i "/path/to/your-key.pem" ubuntu@<PUBLIC_IP_ADDRESS>`.

### Using the Config File in the `.ssh` Folder
1. Create or edit `~/.ssh/config` and add an entry block:
   ```text
   Host aws-server
       HostName 54.210.10.1
       User ubuntu
       IdentityFile ~/.ssh/my-aws-key.pem

