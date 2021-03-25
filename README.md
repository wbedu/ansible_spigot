ansible-spigot
=========
Installs spigot and deploys updated spigot-minecraft server.
By running this role you are accepting [Mojang/Minecraft's eula](https://account.mojang.com/documents/minecraft_eula) and [Spiggot terms](https://www.spigotmc.org/).

Installs pluggins placed in [./files/plugins](./files/plugins)

Requirements
------------
[Debian](https://en.wikipedia.org/wiki/List_of_Linux_distributions#Debian-based) or [RedHat](https://en.wikipedia.org/wiki/List_of_Linux_distributions#RPM-based) System

Role Variables
--------------
```markdown
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
    - role: spigot
      vars:
        gigs: 2
```

Known Issues and Work arounds
-----------------------------

1. requires ops.json file to add a user as an operator.

    * you must add your own ops.json file to the [/files](./files) directory.
    * use [uuid generator](https://mcuuid.net/) to get your uuid
    * example ops.json:
    ```json
    [
      {
        "uuid": "you-own-uuid-goes-here",
        "name": "username",
        "level": 4,
        "bypassesPlayerLimit": true
      }
    ]
    ```

2. dependant on git an custom java roles.
    * it works but contibution is appreciated at [Java role](https://github.com/wbedu/ansible-java) and [git role](https://github.com/wbedu/ansible-git).



License
-------

[GNU GPLv3](https://choosealicense.com/licenses/gpl-3.0/)

Author Information
------------------
[https://github.com/wbedu](https://github.com/wbedu)
