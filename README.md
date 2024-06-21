# **Gitlab Server Install**

**Dependencies**
__________________________________________________________________________________________________

- sudo apt-get update
- sudo apt-get install -y curl openssh-server ca-certificates tzdata perl
- sudo apt-get install -y postfix


**Set gitlab repository**
__________________________________________________________________________________________________
- curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash


**Show available-versions**
__________________________________________________________________________________________________
- apt-cache madison gitlab-ce 


**Check all ports in use**

**Install gitlab-ce package**
_________________________________________________________________________________________________
- sudo EXTERNAL_URL="https or http://ip|domen" apt-get install gitlab-ce



**Install Gitlab-runner**
_________________________________________________________________________________________________
- curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash

- sudo apt-get install gitlab-runner
