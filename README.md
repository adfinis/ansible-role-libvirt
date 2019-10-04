# ROLE libvirt

[![GitHub](https://img.shields.io/github/license/adfinis-sygroup/ansible-role-libvirt.svg?style=flat-square)](https://github.com/adfinis-sygroup/ansible-role-libvirt/blob/master/LICENSE)
[![Travis (.org)](https://img.shields.io/travis/adfinis-sygroup/ansible-role-libvirt.svg?style=flat-square)](https://travis-ci.org/adfinis-sygroup/ansible-role-libvirt)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-adfinis--sygroup.libvirt-660198.svg?style=flat-square)](https://galaxy.ansible.com/adfinis-sygroup/libvirt)

This role configures and manages libvirt.

## Requirements

This role has no additional requirements.

## Role Variables

The following defaults variables can be configured:

``` yaml
# action taken on host boot
# - start   all guests which were running on shutdown are started on boot
#           regardless on their autostart settings
# - ignore  libvirt-guests init script won't start any guest on boot, however,
#           guests marked as autostart will still be automatically started by
#           libvirtd
libvirt_on_boot_action: start

# Number of seconds to wait between each guest start. Set to 0 to allow
# parallel startup.
libvirt_on_boot_delay: 2

# action taken on host shutdown
# - suspend   all running guests are suspended using virsh managedsave
# - shutdown  all running guests are asked to shutdown. Please be careful with
#             this settings since there is no way to distinguish between a
#             guest which is stuck or ignores shutdown requests and a guest
#             which just needs a long time to shutdown. When setting
#             ON_SHUTDOWN=shutdown, you must also set SHUTDOWN_TIMEOUT to a
#             value suitable for your guests.
libvirt_on_shutdown_action: shutdown

# Number of guests will be shutdown concurrently, taking effect when
# "ON_SHUTDOWN" is set to "shutdown". If Set to 0, guests will be shutdown one
# after another. Number of guests on shutdown at any time will not exceed number
# set in this variable.
libvirt_on_shutdown_parallel: 2

# Number of seconds we're willing to wait for a guest to shut down. If parallel
# shutdown is enabled, this timeout applies as a timeout for shutting down all
# guests on a single URI defined in the variable URIS. If this is 0, then there
# is no time out (use with caution, as guests might not respond to a shutdown
# request). The default value is 300 seconds (5 minutes).
libvirt_on_shutdown_timeout: 300

# Allow managing LVM logical volumes with libvirt (for VM storage)?
# Will result in the installation of additional packages on some systems.
libvirt_use_lvm_storage: false
```

For a list OS related variables that usually don't need to be customized have a
look at the vars/ directory.

## Dependencies

This role has no additional dependencies.

## Example Playbook

Below example shows how the role can be integrated into a playbook using
external vars:

``` yaml
- hosts: servers
  roles:
    - { role: adfinis-sygroup.libvirt }
```

## License

[GPL-3.0](https://github.com/adfinis-sygroup/ansible-role-libvirt/blob/master/LICENSE)

## Author Information

libvirt role was written by:

-   Adfinis SyGroup AG \| [Website](https://www.adfinis-sygroup.ch/) \|
    [Twitter](https://twitter.com/adfinissygroup) \|
    [GitHub](https://github.com/adfinis-sygroup)
