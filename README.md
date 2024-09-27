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


**-----Check all ports in use-----**

**Install gitlab-ce package**
_________________________________________________________________________________________________
- sudo EXTERNAL_URL="https or http://ip|domen" apt-get install gitlab-ce
- 
  **Example:** sudo EXTERNAL_URL="http://gitlab.ulugbek.uz" apt-get install gitlab-ce



**Install Gitlab-runner**
_________________________________________________________________________________________________
- curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash

- sudo apt-get install gitlab-runner


**Add gitlab registry via _/etc/gitlab/gitlab.rb_**
_________________________________________________________________________________________________
-
################################################################################
## Container Registry settings
##! Docs: https://docs.gitlab.com/ee/administration/packages/container_registry.html
################################################################################

**registry_external_url '[http://git.ulugbek.uz:5000'**

### Settings used by GitLab application
# gitlab_rails['registry_enabled'] = true
# gitlab_rails['registry_host'] = "registry.gitlab.example.com"
# gitlab_rails['registry_port'] = "5005"
# gitlab_rails['registry_path'] = "/var/opt/gitlab/gitlab-rails/shared/registry"

-
###! Do not change the following 3 settings unless you know what you are
###!   doing
# gitlab_rails['registry_api_url'] = "http://127.0.0.1:5000"
# gitlab_rails['registry_key_path'] = "/var/opt/gitlab/gitlab-rails/certificate.key"
# gitlab_rails['registry_issuer'] = "omnibus-gitlab-issuer"

### Settings used by Registry application
**registry['enable'] = true**
# registry['username'] = "registry"
# registry['group'] = "registry"
# registry['uid'] = nil
# registry['gid'] = nil
# registry['dir'] = "/var/opt/gitlab/registry"
**registry['registry_http_addr'] = "0.0.0.0:5000"**
# registry['debug_addr'] = "localhost:5001"
# registry['log_directory'] = "/var/log/gitlab/registry"
# registry['env_directory'] = "/opt/gitlab/etc/registry/env"
# registry['env'] = {
#   'SSL_CERT_DIR' => "/opt/gitlab/embedded/ssl/certs/"
# }

-
## Registry NGINX
################################################################################

# All the settings defined in the "GitLab Nginx" section are also available in
# this "Registry NGINX" section, using the key registry_nginx.  However, those
# settings should be explicitly set. That is, settings given as
# nginx['some_setting'] WILL NOT be automatically replicated as
# registry_nginx['some_setting'] and should be set separately.

# Below you can find settings that are exclusive to "Registry NGINX"
**registry_nginx['enable'] = false**

# registry_nginx['proxy_set_headers'] = {
#  "Host" => "$http_host",
#  "X-Real-IP" => "$remote_addr",
#  "X-Forwarded-For" => "$proxy_add_x_forwarded_for",
#  "X-Forwarded-Proto" => "https",
#  "X-Forwarded-Ssl" => "on"
# }
-
