# Upgrade to specific OS release

Fully automated upgrading of a Debian system to a specific major version, including intermediate reboots.

Supported upgrade paths start at Debian 8 (jessie), and defaults to upgrading to
Debian 13 (bullseye).

The role will run all the required upgrades in sequence, so:

- Debian 8 systems will go to 9, 10, 11, 12 and end up at Debian 13.
- Debian 9 will go to 10, and then to Debian 11.
- etc

It is also possible to upgrade to an earlier release, for example:

- Debian 9 to Debian 10.

Downgrading is not supported.


This role was created to automate the upgrade of VMs on a platform that only
offered instantiating Debian 9 VMs.
It has been tested on clean VMs only.

# Example playbooks

## Example 1

Upgrade Debian 9 to Debian 11. This includes 2 release upgrades:
- 9 to 10
- 10 to 11

```yaml
- hosts: stretch
  roles:
    - role: ansible_role_release_upgrade
```

## Example 2

Upgrade Debian 8 to Debian 11. This means 3 release upgrades:

```yaml
# - 8 to 9
# - 9 to 10
# - 10 to 11
#
- hosts: jessie
  roles:
    - role: ansible_role_release_upgrade
```

## Example 3

Upgrade Debian 9 to Debian 10. This is just one release upgrade, but because it
is *not* to the default (i.e. latest stable) release, the version has to be
provded:

```yaml
- hosts: stretch
  roles:
    - role: ansible_role_release_upgrade
      vars:
        required_release_version: 10
```

# Testing

```bash
MOLECULE_DISTRO=debian10 molecule test
```

Author Information
------------------

Dick Visser
Benjamin Böhm
Harliff
