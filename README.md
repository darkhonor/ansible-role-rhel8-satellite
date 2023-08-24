# Red Hat Satellite Server

This role will install the Red Hat Satellite Server on a RHEL 8 system.

## Requirements

This role requires a provisioned Red Hat Enterprise Linux 8 (x86_64) system.  Per
the [Red Hat Satellite Documentation](https://access.redhat.com/documentation/en-us/red_hat_satellite/6.13/html/installing_satellite_server_in_a_disconnected_network_environment/preparing_your_environment_for_installation_satellite#doc-wrapper),
the following requirements must be satisfied:

* x86_64 architecture
* The latest version of Red Hat Enterprise Linux 8
* 4-core 2.0 GHz CPU at a minimum
* A minimum of 20 GB RAM is required for Satellite Server to function. In addition, a minimum of 4 GB RAM of swap space is also recommended. Satellite running with less RAM than the minimum value might not operate correctly.
* A unique host name, which can contain lower-case letters, numbers, dots (.) and hyphens (-)
* A current Red Hat Satellite subscription
* Administrative user (root) access
* Full forward and reverse DNS resolution using a fully-qualified domain name

This role will not ensure these requirements are met.  You must verify these prior
to applying this role.  

Furthermore, the RHEL server must be freshly provisioned that has no other roles assigned.  The server requires the `@Base` package group with no other package-set
modifications.  Additionally, no lockdown configurations can be applied at this point.

## Role Variables

The following role variables are **required** to be provided when the role is applied:

```yaml
satellite_iso_mount_src: /dev/sr0
satellite_organization: "SomeOrganization"
satellite_location: "SomeLocation"
satellite_initial_admin_user: "SomeAdmin"
satellite_initial_admin_password: "ChangeMeT0@g00dPassW0rdNow!"
```

The following variables can be set or remain as is depending on your environment:

```yaml
online_instance: false
satellite_iso_mount_point: /media/sat6
satellite_iso_mount_fstype: iso9660
satellite_iso_mount_opts: ro,noauto
```

## Dependencies

There are no other role dependencies required.

## Example Playbook

This playbook will apply this role:

```yaml
- name: Install Red Hat Satellite
  hosts: satellites
  become: true
  gather_facts: true
  role:
    - name: satellite
      satellite_iso_mount_src: /tmp/Satellite-6.13.3-rhel-8-x86_64.dvd.iso
      satellite_organization: "Acme Sporting Goods"
      satellite_location: "Seoul"
      satellite_initial_admin_user: '{{ satellite_admin }}'
      satellite_initial_admin_password: '{{ satellite_admin_pw }}'
```

It is important to note that the `become` parameter is required for this role
to succeed.

## License

MIT

## Author Information

Alex Ackerman, X: @darkhonor
