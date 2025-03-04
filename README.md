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
**Odatda gitlab http url bilan ko'tarilganda Container Registry ko'tarilmaydi. Container Registry ishlashi uchun  gitlab configuratsiyasini change qilish kerak  _/etc/gitlab/gitlab.rb_**

**-- Container Registry settings --**


Container Registry URLi
-   _registry_external_url 'http://git.ulugbek.uz:5000_'       

-  _registry['enable'] = true_

- _registry['registry_http_addr'] = "0.0.0.0:5000_"

Container Registry nginxga bog'lanmasdan to'g'irdan to'g'ri ishlashi uchun
- _registry_nginx['enable'] = false_        



**Restart gitlab-ctl**

     sudo gitlab-ctl reconfigure
#
**Using many runners at the moment - /etc/gitlab-runner/config.toml . Runner nechta bo'lsa n o'rniga shu sonni qo'yish kerak. Bu runnerlarni paralel ishlashi uchun**

  -  _concurrent = n_
#
**Gitlab-runner restart**

    gitlab-runner restart
#
**Gitlab-runnerni  _git.ulugbek.uz/group_name/repo_name_ repositorysiga ulanib push qilishi uchun runnerni configuratsiyasini change qilish kerak  _/etc/gitlab-runner/config.toml_** 

**-- [runners.docker] --**
 
  - extra_hosts = ["git.ulugbek.uz:192.168.15.128"]


gitlab-runner restart

#
**Docker:dindni servrdagi docker enginega bog'lanishi uchun runner configuratsiyasini change qilish kerak  - _/etc/gitlab-runner/config.toml_**

**-- Registry NGINX --**
  - volumes = ["/cashe", "/var/run/docker.sock:/var/run/docker.sock"]
  -  _privileged = true_

Nechta runner bo'sa hammasiga qo'shish kerak

     gitlab-runner restart

#

**Dockerga imageni push yoki pull qilganda default DockerHubga chiqadi. Uni local Gitlabdan http bilan olish uchun Gitlab addresini ko'rsatish kerak. Qaysi serverga Pull qilmoqchi bo'lsa shu server docker configuratsiyasini change qilish kerak _/etc/docker/daemon.json_**
 
  - { "insecure-registries":["git.ulugbek.uz:5000"] }


          sudo service docker restart
#


**Note**

- Qaysi serverga applicationni deploy qilmoqchi bo'lsak. Usha serverda ssh key generatsiya qilinadi. Qilingan keylardagi Public keyni **id_rsa.pub(public)**  shu serverdagi _authorized_keys_ ga ko'chiriladi _**copy cat id_rsa.pub >> authorized_keys**_ qilinadi. Privet keyni **id_rsa(privet)** gitlabdagi repositryga yoki ush repository joylashgan guruhni  **Vareble** qismiga qo'shish kerak.


- Gitlabga pull push qilish uchun Gitlab turgan serverni va Application turgan serverni docker login qilib qo'yish kerak

        docker login git.ulugbek.uz:5000
