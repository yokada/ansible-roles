## References

- [ Best Practices — Ansible Documentation ]( http://docs.ansible.com/ansible/latest/playbooks_best_practices.html )
- [ Ansibleで光の速さのWEBサーバーを光の速さで構成してみる。 - Qiita ]( https://qiita.com/sak_2/items/7dd3dcd864f93103f0db )
- [ NicolasMas/ansible.tomcat: Tomcat 8 playbook for CentOS 7 ]( https://github.com/NicolasMas/ansible.tomcat )

## Create hosts file

```
# hosts
[your-server]
xxx.xxx.xxx.xxx ansible_ssh_private_key_file=~/.ssh/id_rsa ansible_ssh_user=root
```

## Configure group_vars/main.yml

```
$ mv group_vars/all.example group_vars/all
```

```
$ vi group_vars/all
```


## Create playbooks what you need

### init.yml


```
---
- hosts: your-server
  sudo: true
  roles:
    - ssh
    - selinux
```

### site.yml

```
---
- name: Install WordPress, MariaDB, Nginx, and PHP-FPM, Tomcat, Java1.8, Postgresql 9.6
  hosts: your-server
  remote_user:
  sudo: yes
  roles:
    - common
    - mariadb
    - nginx
    - php-fpm
    - wordpress
    - java
    - tomcat
    - postgres
```


## Run playbooks

Dry run:

```shell
$ ansible-playbook -i hosts init.yml site.yml -C
```

Actual run

```shell
$ ansible-playbook -i hosts init.yml site.yml
```
