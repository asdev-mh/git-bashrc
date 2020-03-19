# git-bashrc
use a bashrc for faster commandline

Create File .bashrc in C:\User\USERNAME\

```bash
# Start SSH Agent
#----------------------------

SSH_ENV="$HOME/.ssh/environment"

function run_ssh_env {
  . "${SSH_ENV}" > /dev/null
}

function start_ssh_agent {
  echo "Initializing new SSH agent..."
  ssh-agent | sed 's/^echo/#echo/' > "${SSH_ENV}"
  echo "succeeded"
  chmod 600 "${SSH_ENV}"

  run_ssh_env;

  ssh-add ~/.ssh/id_rsa;
}

if [ -f "${SSH_ENV}" ]; then
  run_ssh_env;
  ps -ef | grep ${SSH_AGENT_PID} | grep ssh-agent$ > /dev/null || {
    start_ssh_agent;
  }
else
  start_ssh_agent;
fi

# ----------------------
# Git Aliases
# ----------------------
alias ga='git add .'
alias gbd='git branch --delete '
alias gc='git commit --message'
alias gco='git checkout'
alias gcob='git checkout -b'
alias gcom='git checkout master'
alias gcos='git checkout staging'
alias gcod='git checkout develop'
alias gs='git status'
alias gp='git pull'
alias gpus='git push --set-upstream origin '
alias gpu='git push'
alias gmp='git checkout master; git pull;'
```
