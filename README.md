ansible-spigot
=========
Installs spigot and deploys updated spigot-minecraft server.
By running this role you are accepting [Mojang/Minecraft's eula](https://account.mojang.com/documents/minecraft_eula) and [Spiggot terms](https://www.spigotmc.org/).

Assumes the approviate version of java is installed. (Java 16 or higher as of Aug 2020)


Installs pluggins placed in [./files/plugins](./files/plugins)

Requirements
------------
[Debian](https://en.wikipedia.org/wiki/List_of_Linux_distributions#Debian-based) or [RedHat](https://en.wikipedia.org/wiki/List_of_Linux_distributions#RPM-based) System

Role Variables
--------------
```yml
---
# vars file for spigot role

#default username that will own and run spigot
admin_username: mcadmin

#default dir that all files will be contained in
spigot_dir: ~/spigot

#default ram used by server instance in gigabytes
gigs: 2

```
see [vars/mail.yml](./vars/main.yml)

Example Playbook
----------------

```yml
---
- hosts: minecraft
  remote_user: root
  become: yes
  become_method: sudo

  roles:
    - role: ansible-spigot
      vars:
        gigs: 2
        op_users:
          - name: user1
            uuid: 7233d292-06b7-4ced-a157-6f07b37fe91c
          - name: user2
            uuid: db6395d8-61a6-4a39-b8e3-891f04270e5c
          - name: user2
            uuid: ee028846-c5f7-4042-808a-45b5a01a214d
```
License
-------

[GNU GPLv3](https://choosealicense.com/licenses/gpl-3.0/)

Author Information
------------------
[https://github.com/wbedu](https://github.com/wbedu)
