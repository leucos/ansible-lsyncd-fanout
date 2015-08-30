ansible-lsyncd-fanout role
==========================

This role will let you replicate multiple directories to multiple
targets, using lsyncd 2.x.


## Variables

`lsyncd_fanout_delay`: delay between file syncs (default: 5)
`lsyncd_fanout_directories`: directories to sync (required, default: false, i.e.
none)
`lsyncd_fanout_max_processes`: max concurrent sync processes (default: 5)
`lsyncd_fanout_slaves_interface`: what network interface do the slave
use to communicate with me (required, default: false, i.e. none)
`lsyncd_fanout_slaves_group`: name of group containing slaves to sync (required, default: none)

## Usage

    - role: ansible-lsyncd-fanout
      lsyncd_fanout_directories:
        - '/var/www/website'
      lsyncd_fanout_slaves_interface: eth0
      lsyncd_fanout_slaves_group: lsyncd-slaves

This will sync directory `/var/www/website` on all hosts in the
`lsyncd-slaves` group, using the slave's IP address on `eth0`. You can
set multiple directories if you have several of them to sync.

## Limitations

This role does not support concurrent lsyncd instances, and as such can
only be executed once in a playbook.
In practice, this means that you can not sync to different sets of
servers depending on the directory.

## Warning

While it's convenient, this role creates a passwordless ssh key to
synchronize remote hosts via rsync+ssh. Filter out and don't loose your private key !


