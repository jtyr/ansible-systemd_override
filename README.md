systemd_override
================

Ansible role which helps to configure Systemd override.

The configuration of the role is done in such way that it should not be
necessary to change the role for any kind of configuration. All can be
done either by changing role parameters or by declaring completely new
configuration as a variable. That makes this role absolutely
universal. See the examples below for more details.

Please report any issues or send PR.


Examples
--------

```yaml
---

- name: Example of how to configure Systemd override
  hosts: all
  vars:
    systemd_override_config:
      # Systemd override for the Filebeat service
      - name: filebeat
        # Content of the override file
        content:
          # This is the [Service] section
          Service:
            # This is the option inside the [Service] section
            LimitNOFILE: 65536
  roles:
    - systemd_override
```


Role variables
--------------

Variables used by the role:

```yaml
# Base directory
systemd_override_dir_base: /etc/systemd

# Sub-directory in the base directory [system|user|network]
systemd_override_dir_subdir: system

# Final directory
systemd_override_dir: "{{ systemd_override_dir_base }}/{{ systemd_override_dir_subdir }}"

# Dir postfix
systemd_override_dir_postfix: d

# Default kind to create override for
systemd_override_kind: service

# Default name of the override file
systemd_override_file: override.conf

# Whether to restart service or not
systemd_override_restart_service: no

# Configuration (see README for more details)
systemd_override_config: []
```


Dependencies
------------

- [`config_encoder_filters`](https://github.com/jtyr/ansible-config_encoder_filters)


License
-------

MIT


Author
------

Jiri Tyr
