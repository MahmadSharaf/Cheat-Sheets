# Git Version Control Cheat sheet

- [Git Version Control Cheat sheet](#git-version-control-cheat-sheet)
  - [Getting started](#getting-started)
    - [Configure your name and public email](#configure-your-name-and-public-email)
    - [How to configure a Bash Profile](#how-to-configure-a-bash-profile)
    - [bash_profile](#bash_profile)
  - [Git commands](#git-commands)
    - [Terminal Commands](#terminal-commands)
    - [Initialize a repository or clone it](#initialize-a-repository-or-clone-it)
    - [Adding files to the repo](#adding-files-to-the-repo)
    - [Check changes](#check-changes)
    - [Tagging](#tagging)
    - [Branching](#branching)
    - [Merging](#merging)
    - [Undoing Changes](#undoing-changes)
    - [Reset](#reset)
    - [Collaboration](#collaboration)
  - [Further Research](#further-research)

## Getting started

### Configure your name and public email

1. To identify yourself locally:

   ```bash
   git config user.name "name"
   # This signs your name locally to current repository with name.

   git config user.email "e-mail"
   # this signs your email locally to current repository with e-mail.
   ```

2. To identify yourself globally:

   ```bash
   git config --global user.name "name"
   #This signs your name globally to current repository with name.
   git config --global user.email "e-mail": this signs your email  globally to current repository with e-mail.
   ```

### How to configure a Bash Profile

1. sets up Git with your name

   ```bash
   git config --global user.name "Your-Full-Name"
   ```

2. sets up Git with your email

   ```bash
   git config --global user.email "your-email-address"
   ```

3. makes sure that Git output is colored

   ```bash
   git config --global color.ui auto
   ```

4. displays the original state in a conflict

   ```bash
   git config --global merge.conflictstyle diff3
   ```

5. display config list

   ```bash
   git config --list
   ```

6. get Git working with your code editor

   ```bash
   #Atom
   git config --global core.editor "atom --wait"
   #Sublime
   git config --global core.editor "'C:/Program Files/Sublime Text 2/sublime_text.exe' -n -w"
   #VSCode
   git config --global core.editor "code --wait"
   ```

### bash_profile

1. First step: Create bash profile:

   ```bash
   nano .bash_profile
   ```

2. Add this line of code at the top of .bash_profile file:

   ```bash
   export PS1=" "
   ```

   What we put between the quotation marks will be what we see before each new command line.  
   In order to see the saved changes, press `ctrl + o` and hit return to save. To exit nano, press `ctrl + x`. In order to view your beautiful work, open a new terminal window or enter `source .bash_profile`.

3. Add additional information:

   - `\u` — Username
   - `\d` — Current date
   - `\t` — Current time as HH:MM:SS
   - `\W` — Current working directory
   - `\w` — Full path of your current working directory
   - `\n` — Adds a new line
   - [SeeMore](https://ss64.com/bash/syntax-prompt.html)

4. Add colors:

   - `\[\e[**m\]` — Think of this like an opening tag
   - `**` — your color code (see below)
   - `\[\e[0m\]` — Closing tag for the color scheme

   Whatever you wrap the `\[\e[**m\]` and `\[\e[0m\]` in will be in the color you designate immediately following `\[\e[**m\]`. Replace the `**` with the desired color codes:

   - 31 — red
   - 32 — green
   - 34 — blue
   - 35 — purple
   - 36 — cyan
   - 37 — white

   You can add a background color to the text starting with `\[\e[**;**m\]`. The first color code will be the text, the second is the background. Some background codes include:

   - 41 — red
   - 42 — green
   - 44 — blue
   - 45 — purple
   - 46 — cyan
   - [See more](http://mybyways.com/blog/os-x-terminal-color-prompt)

Example:

```bash
export PS1="\t \[\e[32m\]\u\[\e[0m\] \[\e[35m\]\w\[\e[0m\] \[\e[36m\]$(__git_ps1)\[\e[0m\] \n $ "
```

## Git commands

### Terminal Commands

- `ls` - used to list files and directories
- `mkdir` - used to create a new directory
- `cd` - used to change directories
- `rm` - used to remove files and directories

### Initialize a repository or clone it

```bash
# To create a new repository with Git —​ you may notice a new directory created, named ".git"
git init

# Clone a repository into a new directory(could be a link or path).
git clone [remote_repo_link]
# clone the project and have it use a different name all in one go
git clone [remote_repo_link] [new_name]
```

### Adding files to the repo

```bash
# Add all files that have changes to the temporary stage
git add .
# Add file_name to the temporary stage.
git add [file_name]
# This permanently stores the contents of the index in the repository.
git commit [file_name]
# This  will automatically notice any modified (but not new) files, add them to the index, and commit, all in one step.
git commit -a
# to tell Git about the files that Git should not track.
.gitignore [file_1] [file_2] ... [file_n]
```

### Check changes

```bash
# Show commit logs.
git log
# shows the commit logs in tree-view.
git log --graph
# Lists one commit per line. Show first 7 characters of SHA and the commit message
git log --newline
# Shows all commits of all branches.
git log --all
# shows only the most recent log.
git log -n 1
# complete diffs at each step.
git log -p
# the overview of the change is useful to get a feel of each step.
git log --stat --summary
# Group by contributor commits.
git shortlog
# -n show just the number of commits, -n arrange it numerically
git shortlog -s -n
# Filter By Author
git log --author=[author_name]
# Filter commits by the provided message part.
git log --grep=[part_of_commit_message]
# shows a specific commit
git show [SHA]
# Show changes between commits, commit and working tree, etc
git diff
# changes between first and second ids.
git diff [first_id] [second_id]
# You can see what is about to be committed using git diff with the --cached option.
git diff --cached
# Show the working tree status
git status
```

### Tagging

```bash
# Adds a tag to current commit.
git tag [version_number ex:v1.0]
# RECOMMENDED because Annotated tags include (the person who made the tag, the date the tag was made, a message for the tag)
git tag -a v1.0
# fetches all the available tags for this repository.
git tag
# Adding A Tag To A Past Commit
git tag -a v1.0 a87984
# Deletes the tag
git tag -d v1.0
```

### Branching

```bash

# shows the available branches and identify the current branch with '*'.
git branch
# creates new branch with branch_name.
git branch [branch_name]
# Creates a new branch and switches to it.
git checkout -b [branch_name]
# deletes branch_name
git branch -d [branch_name]
# switch to the branch_name branch.
git checkout [branch_name]
```

### Merging

```bash
# merges two branches together
git merge [first_branch] [second_branch]
# This command undo the merge
git reset --hard HEAD^
```

### Undoing Changes

```bash
# alter the most-recent commit.
git commit --amend
# Creates a new snapshot with a revert changes of the given SHA commit
git revert [SHA-of-commit-to-revert]
# open the editor to change the message.
git revert [SHA-of-commit-to-revert] -e / --edit
# Will not open the editor.
git revert [SHA-of-commit-to-revert] --no-edit
# will add the changes to the staging index
git revert [SHA-of-commit-to-revert] -n / --no-commit
```

### Reset

```bash
# The git reset command is used to erase commits:
git reset <reference-to-commit>:
# It can be used to:
# move the HEAD and current branch pointer to the referenced commit
# erase commits with the --hard flag
# moves committed changes to the staging index with the --soft flag
# unstages committed changes --mixed flag
# Typically, ancestry references are used to indicate previous commits.
# The ancestry references are:
# ^ – indicates the parent commit
# ~ – indicates the first parent commit
```

### Collaboration

```bash
# to view and create remotes
git remote
# To add this repository on GitHub as a remote.
git remote add [referral_name] [remote_repo_link]
# v stands for verbose that means that git will get more information.
git remote -v
#
git remote rename [old_name] [new_name]
# to send my changes to the remote
git push [referral_name] [branch_name]
# to pull changes on branch_name locally
git pull [referral_name] [branch_name]
# pushes modified code to your remote repo.
bash file_name.sh [remote_repo_link]
# gets a sneak peak of the log of the remotely repo.
git fetch [referral_name]
# do the same as git pull but without the merging step
git fetch [referral_name] [branch_name]
# merges the commits on the local with remote repos.
git merge [branch_name] [referral_name/branch_name]
# disconnect local git repo from remote master
git remote rm origin
```

## Further Research

- [Git Internals - Plumbing and Porcelain](https://git-scm.com/book/en/v2/Git-Internals-Plumbing-and-Porcelain)
- [Customizing Git - Git Hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)
