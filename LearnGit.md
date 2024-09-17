# Table of Contents

1. [Install Git](#install-git)
2. [Configure Git](#configure-git)
3. [Create a new repository](#create-a-new-repository)
4. [Git commands for adding, committing, and managing changes](#git-commands-for-adding-committing-and-managing-changes)
5. [Git commands for managing remote repositories](#git-commands-for-managing-remote-repositories)
6. [Push the changes to the remote repository](#push-the-changes-to-the-remote-repository)
7. [Branch management](#branch-management)
8. [Recommended resouces for git learning](#recommended-resouces-for-git-learning)


## Install Git

### Macos

1. instal git through homebrew

```bash
brew install git
```

then check if git is installed

```bash
git --version
```

2. install XCode from App Store, which also install git. Then choose "Xcode" -> "Preferences", find "Downloads" tab, and choose "Command Line Tools" then click "Install".

### Windows

1. Download and install Git from [here](https://gitforwindows.org/)

2. Check if Git is installed

```bash
git --version
```

## Configure Git

```bash
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```

## Create a new repository

Use `cd` to choose a directory to store the repository:

```bash
cd /path/to/your/directory
```

Then initialize the repository:

```bash
git init
```

## Git commands for adding, committing, and managing changes

1. `git status` - show the status of the repository
2. `git add <file>` - add a file to the repository
3. `git commit -m "commit message"` - commit the changes
4. `git log` - show the commit history
5. `git diff` - show the changes
6. `git reset --hard HEAD^` - trace back to the previous commit, or use `HEAD~2` to trace back to the second previous commit and so on.
7. `git reset --hard <commit>` - trace back to the specified commit
8. `cat <file>` - show the content of the file
9. `git checkout -- <file>` - discard the changes in the working directory
10. `rm <file>` - remove a file from the working directory
11. `git rm <file>` - remove a file from the repository

## Git commands for managing remote repositories

First you should create a ssh key for your local machine:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
# -b stands for "bits" and specifies the key size (4096 bits in this case)
# -C stands for "comment" and is typically used to add a label (usually an email address)
```

then you should add the ssh key to ssh agent:
1. run ssh agent:
```bash
eval "$(ssh-agent -s)"
```

2. add the ssh key to ssh agent:

```bash
ssh-add ~/.ssh/id_rsa
```

3. configure using ssh key to sign commit and push:

```bash
git config --global gpg.format ssh
```

4. set the ssh key to the git config:

```bash
git config --global user.signingkey /path/to/your/ssh/key.pub
```
then open the .gitconfig file and add the following:
```
[commit]
  # GPG signing key
  gpgsign = true
[tag]
  gpgsign = true
```

5. add ssh key to github account:
Open rsa.pub file and copy the content, then go to github -> settings -> SSH and GPG keys -> New SSH key, paste the content and save. There are two kinds of ssh keys, one for connectiong to github server, another for signing commit. Make sure both are added.

6. Test the connection to github server:

```bash
ssh -T git@github.com
```
It will prompt you to confirm the connection. After you have check the [github key fingerpint](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints) is right, type "yes" and press Enter.

## Push the changes to the remote repository:

There are two ways to push the changes to the remote repository:
1. Create a new repository on github, then push the changes to the remote repository:

```bash
git remote add origin git@github.com:username/repository.git
git branch -M main
git push -u origin main

# The -M option in the previous command (git branch -M main) means:
# -M: Rename the current branch to 'main', even if the branch already exists.
# It's equivalent to --move --force.
# This is commonly used to rename the default branch from 'master' to 'main'.
```
2. Clone the existing repository (for example,  "git") to local machine, then push the changes to the remote repository:
```
git clone git@github.com:username/repository.git
cd repository
git branch -M main
git push -u origin main
```

Command lines to pull the changes from the remote repository:
```
git pull

# The 'git pull' command is used to fetch and download content from a remote repository 
# and immediately update the local repository to match that content. It's essentially 
# a combination of 'git fetch' followed by 'git merge'.

# Here's a breakdown of what 'git pull' does:
# 1. It fetches the specified remote's copy of the current branch.
# 2. It merges it into the local copy of the current branch.

# Usage:
# git pull [<options>] [<repository> [<refspec>...]]

# Common options:
# --rebase: Instead of merging, rebase the current branch on top of the upstream branch
# --no-commit: Perform the merge but don't automatically commit
# --ff-only: Only fast-forward if possible

# Examples:
# git pull                     # Pull from the default remote (usually 'origin')
# git pull origin main         # Pull from the 'main' branch of the 'origin' remote
# git pull --rebase origin dev # Pull and rebase from the 'dev' branch of 'origin'

# It's good practice to use 'git pull' before pushing your changes to ensure 
# you're working with the latest version of the code.
```

the following command lines are from github official documentation:
1. create a new repository on the command line
```
echo "# Git" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin YourRepositoryURL
git push -u origin main
```

2. push an existing repository from the command line
```
git remote add origin YourRepositoryURL
git branch -M main
git push -u origin main
```

### Branch management
1. `git branch` - list all branches
2. `git branch -b <branch>` - create a new branch
3. `git checkout <branch>` - switch to the branch
4. `git merge <branch>` - merge the branch to the current branch
5. `git branch -d <branch>` - delete the branch

## Recommended resouces for git learning
1. [git-flight-rules](https://github.com/k88hudson/git-flight-rules) - a guide for git commands
2. [git-cheat-sheet](https://education.github.com/git-cheat-sheet-education.pdf) - a cheat sheet for git commands

reference:
1. https://liaoxuefeng.com/books/git/introduction/index.html
2. https://blog.csdn.net/m0_52559040/article/details/131426957