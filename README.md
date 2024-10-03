# **Gitlab Server Install**

**Dependencies**

     sudo apt-get update
     sudo apt-get install -y curl openssh-server ca-certificates tzdata perl
     sudo apt-get install -y postfix
#
**Set gitlab repository**

     curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
#
**Show available-versions**

     apt-cache madison gitlab-ce 

#
**Check all ports in use**
#
**Install gitlab-ce package**

    sudo EXTERNAL_URL="https or http://ip|domen" apt-get install gitlab-ce
 
    **Example:** 
    
    sudo EXTERNAL_URL="http://gitlab.ulugbek.uz" apt-get install gitlab-ce
#
**Install Gitlab-runner**

    curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash

    sudo apt-get install gitlab-runner
#
**Add gitlab registry via _/etc/gitlab/gitlab.rb_**

**-- Container Registry settings --**

-   _registry_external_url 'http://git.ulugbek.uz:5000_'

-  _registry['enable'] = true_

- _registry['registry_http_addr'] = "0.0.0.0:5000_"

**-- Registry NGINX --**

- _registry_nginx['enable'] = false_

**Restart gitlab-ctl**

     sudo gitlab-ctl reconfigure
#
**Using many runners at the moment - /etc/gitlab-runner/config.toml**

  -  _concurrent = n_
#
**Gitlab-runner restart**

    gitlab-runner restart
#
**Docker:dind connect server docker engine - /etc/gitlab-runner/config.toml**

**-- Registry NGINX --**
  - volumes = ["/cashe", "/var/run/docker.sock:/var/run/docker.sock"]
  -  _privileged = true_

Nechta runner bo'sa hammasiga qo'shish kerak

     gitlab-runner restart

#
**Gitlab-runnerni  git.ulugbek.uz/git/dev repositoryga ulash  /etc/gitlab-runner/config.toml** 

**-- [runners.docker] --**
 
  - extra_hosts = ["git.ulugbek.uz:192.168.15.128"]
    

        gitlab-runner restart
#
**Dockerga Registrni qayerdan olishni ko'rsatish /etc/docker/daemon.json**
 
  - { "insecure-registries":["git.ulugbek.uz:5000"] }


          sudo service docker restart
#
**Gitlabdan imagelarni pull-push uchun server(host)dan ham gitlabga Login qilip qo'yish kerak**

     docker login git.ulugbek.uz:5000

#
**.TXT**

Groupdagi projectni (repository)ni **Vareble**ga contener ko'tariladigan host serverni **id_rsa(privet)** keyini qo'shamiz.

Gitlabni ssh qismiga kod **push** qilinadigan PCni va **pull** qilinadigan host serverni **id_rsa.pub(public)** keyini qo'shamiz.
