Ansible role to configure some Red Hat based system packages and rules.
This role was based on the awesome job by https://github.com/kleinstuff

Created by Lucas Afonso Kremer

https://www.linkedin.com/in/lucasafonsokremer

Requirements
------------

Ansible:

* ansible-2.8 or higher

Variables:

* The user to be configured and used by ansible.
        ansible_centos_base__username: ansible

* ansible_centos_base__root_login = You should use 'yes' or 'no'. For example, when the bool was 'yes', the sshd config will allow root login from ssh.

* authorized_keys file = One ssh public key or more should be setup on file authorized_keys.
       

       Example:
       ## USERNAME
       ssh-rsa...

       ## USERNAME2
       ssh-rsa...

Role Variables
--------------

* Disable root account
        ansible_centos_base__disable_root_user: 'yes' or 'no', when this parameter was set to 'no', the root user account will remain active. By default, this var value is 'no'.

* Set umask to 077
        ansible_centos_base__improve_umaskto_077 if defined, will set "umask" on /etc/profile to "umask 077". Insert 'yes' on this var if you wanted.

* Default system timezone
        ansible_centos_base__timezone_saopaulo: 'America/Sao_Paulo'

* If defined, the Sao_Paulo timezone will be skiped and used only the new var
        ansible_centos_base__timezone: 'Asia/Tokyo'


Role Informations
--------------

* Tested on: CentOS 7 and CentOS 8

* You can populate /etc/chrony.conf with your own ntp server information

* Basic set of system packages for CentOS 8

```        
        ansible_centos_base__packages_centos8:
  	  - git
  	  - sudo
  	  - vim-enhanced
  	  - which
 	  - mlocate
  	  - setroubleshoot-*
  	  - python3-firewall
  	  - python3-pip
  	  - python3-virtualenv
  	  - gnupg
  	  - aide
  	  - openssl
  	  - rsyslog
  	  - logrotate
  	  - tzdata
  	  - chrony
  	  - audispd-plugins
```

* Basic set of system packages for CentOS 7

```
        ansible_centos_base__packages_centos7:
  	  - git
  	  - sudo
  	  - vim-enhanced
  	  - which
          - yum-plugin-keys
 	  - mlocate
  	  - setroubleshoot-*
  	  - python-firewall
  	  - python-pip
  	  - python-virtualenv
  	  - gnupg
  	  - aide
  	  - openssl
  	  - rsyslog
  	  - logrotate
  	  - tzdata
  	  - chrony
```

* Install extra packages

```
        ansible_centos_base__packages_extra:
          - kernel-doc
          - bind-utils
          - tcpdump
          - tuned-utils
          - strace
          - ltrace
          - bash-completion
          - yum-utils
          - lsof
```

*  Task to disable various kernel modules

```
        ansible_centos_base__modules_to_disable:
  	  - cramfs
          - freevxfs
          - jffs2
          - hfs
          - hfsplus
          - squashfs
          - udf
          - dccp
          - sctp
          - rds
          - tipc
          - firewire-core
          - usb-storage
          - net-pf-31
          - bluetooth
```

Dependencies
------------

This role has no dependencies, but remember to read the item **#Requirements** and **#Role Informations** above.

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: ansible-centos-base-setup }

#ToDo
-----
 - Configure tuned to improve the server performance
 - Configure automatic tests using TravisCI
 - Allow creating more users
 - Allow optional firewalld configuration

License
-------

GPLv3

Author Information
------------------

You can ask me anything using my linkedin or e-mail
