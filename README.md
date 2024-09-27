# **Gitlab Server Install**

**Dependencies**

- sudo apt-get update
- sudo apt-get install -y curl openssh-server ca-certificates tzdata perl
- sudo apt-get install -y postfix
#
**Set gitlab repository**

- curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
#
**Show available-versions**

- apt-cache madison gitlab-ce 

#
**-----Check all ports in use-----**
#
**Install gitlab-ce package**

- sudo EXTERNAL_URL="https or http://ip|domen" apt-get install gitlab-ce
- 
  **Example:** sudo EXTERNAL_URL="http://gitlab.ulugbek.uz" apt-get install gitlab-ce
#
**Install Gitlab-runner**

- curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash

- sudo apt-get install gitlab-runner
#
**Add gitlab registry via _/etc/gitlab/gitlab.rb_**

    **-- Container Registry settings --**

- _registry_external_url 'http://git.ulugbek.uz:5000_'

- _registry['enable'] = true_

- _registry['registry_http_addr'] = "0.0.0.0:5000_"

  **-- Registry NGINX --**

- _registry_nginx['enable'] = false_

**Restart gitlab-ctl**

- sudo gitlab-ctl reconfigure

