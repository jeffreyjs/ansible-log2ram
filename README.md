# Ansible Role: log2ram

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This role installs and configures [log2ram](https://github.com/azlux/log2ram) on Linux systems. Most common for use on systems which use an SD Card, for example a Raspberry-Pi.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

Set to enable log2ram on boot.

```yaml
log2ram_enable_on_boot: true
```

Reboot the machine after instralling `log2ram` or not. It is recommended to reboot the machine after installing. Ansible will wait for the systems to come up and continue with the rest of the tasks.

```yaml
log2ram_reboot_after_install: true
```

Install state, possible values are:
`install` to install log2ram, `remove` to uninstall log2ram, and `update` to update log2ram.

```yaml
log2ram_state: install
```

The ramdisk size. **Note** This should be set to a value > 40M!

```yaml
log2ram_size: "40M"
```

Whether to use `rsync` instead of `cp`. It is recommended to use `rsync` for better performance.

```yaml
log2ram_use_rsync: "true"
```

If set to `false`, the error system mail will be disabled if there's not enough space in RAM.

```yaml
log2ram_mail: "false"
```

Path where logs are saved.

```yaml
log2ram_path_disk: "/var/log"
```

Whether to enable `zram` compatibility. **Note** that zram **must** be enabled and configured on the device if you want to use this.

```yaml
log2ram_use_zl2r: "false"
```

The compression algorithm used for zram. See the `log2ram` [README](https://github.com/azlux/log2ram#install) for more information.

```yaml
log2ram_compression_algorithm: "lz4"
```

Uncompressed zram size.

```yaml
log2ram_log_disk_size: "100M"
```

## Dependencies

None.

## Example Playbook

The following is an example of how to use this role:

```yaml
- hosts: server
  vars_files:
    - vars/main.yml

  roles:
    - role: jeffreyjs.log2ram

  vars:
    log2ram_enable_on_boot: true
    log2ram_reboot_after_install: true
    log2ram_size: "50M"
    log2ram_use_rsync: "false"
    log2ram_mail: "true"
    log2ram_path_disk: "/var/log"
    log2ram_use_zl2r: "false"
    log2ram_compression_algorithm: "lz4"
```

## License

MIT / BSD

## Author Information

[Jeffrey Swindel](https://github.com/jeffreyjs)
