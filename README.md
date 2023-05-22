# Dotfiles

This is my perferred inital setup. 

## What's in it

Here is a list of things I like to have:

### WSL setup

I need to use Windows for work so setting up WSL requires some hoops and admin access. How ever it 
now pretty straight forward. 

https://learn.microsoft.com/en-us/windows/wsl/install


### SSH

Set up SSH by running `ssh-keygen -t ed25519 -C "email@host.com"`

If two keys are needed create them with different names and then create a `.ssh/config` file.

```
# Github
Host github
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_github
  UserKnownHostsFile ~/.ssh/known_hosts
  IdentitiesOnly yes

# Bitbucket
Host bitbucket
  HostName bitbucket.org
  User git
  IdentityFile ~/.ssh/id_ed25519_bitbucket
  UserKnownHostsFile ~/.ssh/known_hosts
  IdentitiesOnly yes

```

### Tmux

My choice of multiplexer. I'm currently trying TPM as a package manager.

#### Installation

`sudo apt install tmux`

#### Usage

Tmux uses a "prefix" to provide access tmux controls. I use the default which is <C-b> (Ctrl+b)
 

### Bash

For the Git branch on the prompt find you PS1 declaration and replace it with:
`PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u\[\033[00m\]$(__git_ps1 "(%s)"):\[\033[01;34m\]\w\[\033[00m\]\$ '`

Add these lines to the bottom of your `.bashrc` if not already present:

```
# to be added at the bottom of your .bashrc

if command -v tmux &> /dev/null && [ -n "$PS1" ] && [[ ! "$TERM" =~ screen ]] && [[ ! "$TERM" =~ tmux ]] && [ -z "$TMUX" ]; then
  exec tmux
fi

if [ -z "$SSH_AUTH_SOCK" ] ; then
  eval `ssh-agent -s`
  ssh-add .ssh/id_ed25519_github
  ssh-add .ssh/id_ed25519_bitbucket
fi
```




https://stackoverflow.com/questions/29725235/add-ssh-key-for-both-github-and-bitbucket-in-single-pc
https://www.gnu.org/software/bash/manual/html_node/Bash-Startup-Files.html
https://stackoverflow.com/questions/15883416/adding-git-branch-on-the-bash-command-prompt
