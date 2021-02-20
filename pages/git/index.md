---
title: Mort9 Posts
author: Mortie Torabi 
---

# Git + Tips and Tricks

**Git** is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency. *Git* is easy to learn and has a tiny footprint with lightning fast performance. ~ [Git-SCM](git-scm.com)

## Managing Multiple Git Repositories with Multiple Private Keys on the same Machine

### 1. Environment variable `GIT_SSH_COMMAND`:

```
GIT_SSH_COMMAND="ssh -i ~/.ssh/id_rsa_example" git clone example
```

Note that `-i` can sometimes be overridden by your config file, in which case, you should give SSH an empty config file, like this:

```
GIT_SSH_COMMAND="ssh -i ~/.ssh/id_rsa_example -F /dev/null" git clone example
```

### 2. Configuration `core.sshCommand`:

```
git config core.sshCommand "ssh -i ~/.ssh/id_rsa_example -F /dev/null"
git pull
git push
```

### 3.  Global Configuration `config` file

1. Configure the `~/.ssh/config` with different Hosts but same HostNames.
2. Clone your repo using the appropriate host.

Example:

```
Host work
 HostName github.com
 IdentityFile ~/.ssh/id_rsa_work
 User git

Host personal
 HostName github.com
 IdentityFile ~/.ssh/id_rsa_personal
 User git
```

And then try to access the repositories like this :

```
git clone git@work:username/my-work-project.git
git clone git@personal:username/my-personal-project.git
```

## Removing Sensitive Data from Git Repository

[Removing sensitive data from a repository - GitHub Docs](https://docs.github.com/en/github/authenticating-to-github/removing-sensitive-data-from-a-repository)