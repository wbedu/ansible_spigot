# ansible_spigot
* * *

Installs spigot and deploys updated spigot-minecraft server.
By running this role you are accepting [Mojang/Minecraft's eula](https://account.mojang.com/documents/minecraft_eula) and [Spiggot terms](https://www.spigotmc.org/).

Assumes the approviate version of java is installed. (Java 16 or higher as of Aug 2020)

Installs plugins placed in [./files/plugins](https://github.com/wbedu/ansible_spigot/tree/master/files/plugins)


## Table of Contents

- [Introduction](#ansible_spigot)
- [Requirements](#Requirements)
- [Variables](#Role-Variables)
- [How to Use](#How-to-Use)
- [Example Playbook](#Example-Playbook)
- [License](#License)
- [Author Information](#Author-Information)
## Requirements

* * *

[Debian](https://en.wikipedia.org/wiki/List_of_Linux_distributions#Debian-based) or [RedHat](https://en.wikipedia.org/wiki/List_of_Linux_distributions#RPM-based) System

## Role Variables

```yml
# default username that will own and run spigot
admin_username: mcadmin

# default dir that all files will be contained in
spigot_dir: $HOME/spigot

# default ram used by server instance in gigabytes
gigs: 2

# server operators
op_users: []

# path that java is installed at
# defaults to attempt useing PATH variable
java_path: "java"

```

see [vars/mail.yml](https://github.com/wbedu/ansible_spigot/blob/master/vars/main.yml)

## How to Use

1.  run galaxy install

   `$ ansible-galaxy install wbedu.ansible_spigot`

2. set your server operators in a Variables

```yml
vars:
  op_users:
    - name: user1
      uuid: 7233d292-06b7-4ced-a157-6f07b37fe91c
```

Note: you can find your uuid using the mojang api here https://api.mojang.com/users/profiles/minecraft/name replace name with your minecraft user name or try sites like [https://mcuuid.net/](https://mcuuid.net/) and [https://minecraftuuid.com/](https://minecraftuuid.com/)

2.  Create a playbook like below and run


## Example Playbook

* * *

```yml
---
- hosts: ansible_test
  remote_user: root
  become: true
  become_method: sudo

  tasks:
    - name: "install java (redhat)"
      package:
        name: java-latest-openjdk
      when: ansible_os_family == "RedHat"
    - name: "install java (Debian)"
      package:
        name: openjdk-16-jdk-headless
      when: ansible_os_family == "Debian"
    - name: "run ansible_spigot role"
      import_role:
        name: wbedu.ansible_spigot
      vars:
        gigs: 1
        op_users:
          - name: user1
            uuid: 7233d292-06b7-4ced-a157-6f07b37fe91c
```

## License

* * *

[GNU GPLv3](https://choosealicense.com/licenses/gpl-3.0/)

## Author Information

<https://github.com/wbedu>
