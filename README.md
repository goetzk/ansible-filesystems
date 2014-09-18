Filesystems
===========

Basic management of filesystems.

Requirements
------------

This role requires at least the following filesystems (and that they have a
label applied before use).
* Root filesystem (to be marked read only)
* Home filesystem (which will remain r/w)
* var filesystem  (which will remain r/w)

If you wish you could partially work around the requirement for the second r/w
partition by making home and var the same filesystem by bind mounting them
before running this role.

If the role is run without updating filesystems_configuration_mounted to
'mounted' filesystems will need to be manually remounted or the server rebooted
to pick up the new configuration. The current setting is the safe default.

Role Variables
--------------

# Read only filesystems
filesystems_configuration_ro: []
# noexec filesystems
filesystems_configuration_noexec: []
# Present updates configuration. Set to 'mounted' to have filesystems remounted
# at once, see mount module docs for explanation and other options
filesystems_configuration_mounted: 'present'
# Move roots home
filesystems_ro_move_root: true

# These two are set per ansible_distribution; these are Debians settings as its
# the only currently enabled distribution.
# Options for filesystems mounted noexec
filesystems_noexec_opts: 'noexec,nosuid'
# Options for filesystems mounted read only
filesystems_rofs_opts: 'ro,data=writeback,errors=remount-ro'


Dependencies
------------

N/A

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      vars:
       - filesystems_configuration_ro:
         - { name: '/', label: 'ROOTFS', filesystem: 'ext4' }
       - filesystems_configuration_noexec:
         - { name: '/tmp', label: 'TEMPFS', filesystem: 'tmpfs'}
       - filesystems_ro_move_root: true
      roles:
         - { role: goetzk.filesystems }

License
-------

GPL2+

Author Information
------------------

Issues or feedback can be reported to the author at karl@kgoetz.id.au; please
prefix the subject with 'ansible' or 'role'.

