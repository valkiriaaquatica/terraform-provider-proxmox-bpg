--- 
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "virtual_environment_cluster_options Resource - terraform-provider-proxmox"
subcategory: ""
description: |-
  This resource creates and manages a Proxmox virtual environment cluster options.
---
---
layout: page
title: proxmox_virtual_environment_cluster_options
parent: Resources
subcategory: Virtual Environment
description: |-
  Manages Proxmox VE Cluster Datacenter options.
---

# Resource: proxmox_virtual_environment_cluster_options

Manages Proxmox VE Cluster Datacenter options.

## Example Usage

```terraform
resource "proxmox_virtual_environment_cluster_options" "options" {
  language                  = "en"
  keyboard                  = "pl"
  email_from                = "ged@gont.earthsea"
  bandwidth_limit_migration = 555555
  bandwidth_limit_default   = 666666
  max_workers               = 5
  migration_cidr            = "10.0.0.0/8"
  migration_type            = "secure"
  next_id = {
    lower = 100
    upper = 999999999
  }
  notify = {
    ha_fencing_mode            = "never"
    ha_fencing_target          = "default-matcher"
    package_updates            = "always"
    package_updates_target     = "default-matcher"
    package_replication        = "always"
    package_replication_target = "default-matcher"
  }
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Optional

- `bandwidth_limit_clone` (Number) Clone I/O bandwidth limit in KiB/s.
- `bandwidth_limit_default` (Number) Default I/O bandwidth limit in KiB/s.
- `bandwidth_limit_migration` (Number) Migration I/O bandwidth limit in KiB/s.
- `bandwidth_limit_move` (Number) Move I/O bandwidth limit in KiB/s.
- `bandwidth_limit_restore` (Number) Restore I/O bandwidth limit in KiB/s.
- `console` (String) Select the default Console viewer. Must be `applet` | `vv`| `html5` | `xtermjs`. You can either use the builtin java applet (VNC; deprecated and maps to html5), an external virt-viewer compatible application (SPICE), an HTML5 based vnc viewer (noVNC), or an HTML5 based console client (xtermjs). If the selected viewer is not available (e.g. SPICE not activated for the VM), the fallback is noVNC.
- `crs_ha` (String) Cluster resource scheduling setting for HA. Must be `static` | `basic` (default is `basic`).
- `crs_ha_rebalance_on_start` (Boolean) Cluster resource scheduling setting for HA rebalance on start.
- `description` (String) Datacenter description. Shown in the web-interface datacenter notes panel. This is saved as comment inside the configuration file.
- `email_from` (String) email address to send notification from (default is root@$hostname).
- `ha_shutdown_policy` (String) Cluster wide HA shutdown policy (). Must be `freeze` | `failover` | `migrate` | `conditional` (default is `conditional`).
- `http_proxy` (String) Specify external http proxy which is used for downloads (example: `http://username:password@host:port/`).
- `keyboard` (String) Default keyboard layout for vnc server. Must be `de` | `de-ch` | `da` | `en-gb` | `en-us` | `es` | `fi` | `fr` | `fr-be` | `fr-ca` | `fr-ch` | `hu` | `is` | `it` | `ja` | `lt` | `mk` | `nl` | `no` | `pl` | `pt` | `pt-br` | `sv` | `sl` | `tr`.
- `language` (String) Default GUI language. Must be `ca` | `da` | `de` | `en` | `es` | `eu` | `fa` | `fr` | `he` | `it` | `ja` | `nb` | `nn` | `pl` | `pt_BR` | `ru` | `sl` | `sv` | `tr` | `zh_CN` | `zh_TW`.
- `mac_prefix` (String) Prefix for autogenerated MAC addresses.
- `max_workers` (Number) Defines how many workers (per node) are maximal started on actions like 'stopall VMs' or task from the ha-manager.
- `migration_cidr` (String) Cluster wide migration network CIDR.
- `migration_type` (String) Cluster wide migration type. Must be `secure` | `insecure` (default is `secure`).
- `next_id` (Attributes) The ranges for the next free VM ID auto-selection pool. (see [below for nested schema](#nestedatt--next_id))
- `notify` (Attributes) Cluster-wide notification settings. (see [below for nested schema](#nestedatt--notify))

### Read-Only

- `id` (String) The unique identifier of this resource.

<a id="nestedatt--next_id"></a>
### Nested Schema for `next_id`

Optional:

- `lower` (Number) The minimum number for the next free VM ID. Must be higher or equal to 100
- `upper` (Number) The maximum number for the next free VM ID. Must be less or equal to 999999999


<a id="nestedatt--notify"></a>
### Nested Schema for `notify`

Optional:

- `ha_fencing_mode` (String) Cluster-wide notification settings for the HA fencing mode. Must be `always` | `never`.
- `ha_fencing_target` (String) Cluster-wide notification settings for the HA fencing target.
- `package_updates` (String) Cluster-wide notification settings for package updates. Must be `auto` | `always` | `never`.
- `package_updates_target` (String) Cluster-wide notification settings for the package updates target.
- `replication` (String) Cluster-wide notification settings for replication. Must be `always` | `never`.
- `replication_target` (String) Cluster-wide notification settings for the replication target.

## Import

Import is supported using the following syntax:

```shell
#!/usr/bin/env sh
# Cluster options are global and can be imported using e.g.:
terraform import proxmox_virtual_environment_cluster_options.options cluster
```
