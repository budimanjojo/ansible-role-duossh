Ansible Duo SSH Role
====================

Role to configure SSH using Duo Security. This role will install duo_unix using the [official Duo documentation](https://duo.com/docs/duounix). **Note**: this role will disable SELinux if you are running Redhat based OS (it is possible to do this without disabling SELinux, but I don't have any interest in doing that, PR is welcomed :D)

Supported OS Families
---------------------

- Ubuntu (tested)
- Arch Linux (tested)
- Redhat (tested)

Role Variables
--------------

Available variables are listed below, the default values are in [defaults/main.yml](./defaults/main.yml):
```
duossh_duosecurity_version: duo version to install, currently at duo_unix-1.11.4 (string)
duossh_duosecurity_checksum: checksum for the tarball which you want to install, can be found at https://duo.com/docs/checksums#duo-unix (string)

# List of configure option to build the binary, ignore if you are not sure
duossh_duosecurity_configure_options: []

duossh_duo_ikey: duo integration key (string)
duossh_duo_skey: duo secret key (string)
duossh_duo_host: duo API hosname (string)
duossh_require_both: whether to require both public key and duo to authenticate to ssh, default to false (bool)

# Dict of duo options, ignore if you are not sure
duossh_duo_options:
```

Dependencies
------------

None

Example Playbook
----------------

Here is an example playbook:
```
- hosts: all

  vars:
    duossh_duo_ikey: {{ secret_duo_ikey }}
    duossh_duo_skey: {{ secret_duo_skey }}
    duossh_duo_host: {{ secret_duo_host }}
    duossh_duo_options:
      failmode: safe

  roles:
  - budimanjojo.duo_ssh
```

License
-------

MIT License
