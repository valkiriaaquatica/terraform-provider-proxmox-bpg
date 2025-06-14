--- 
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "virtual_environment_download_file Resource - terraform-provider-proxmox"
subcategory: ""
description: |-
  This resource creates and manages a Proxmox virtual environment file.
---
---
layout: page
title: proxmox_virtual_environment_download_file
parent: Resources
subcategory: Virtual Environment
description: |-
  Manages files upload using PVE download-url API. It can be fully compatible and faster replacement for image files created using proxmox_virtual_environment_file. Supports images for VMs (ISO images) and LXC (CT Templates).
---

# Resource: proxmox_virtual_environment_download_file

Manages files upload using PVE download-url API. It can be fully compatible and faster replacement for image files created using `proxmox_virtual_environment_file`. Supports images for VMs (ISO images) and LXC (CT Templates).

~> Besides the `Datastore.AllocateTemplate` privilege, this resource requires both the `Sys.Audit` and `Sys.Modify` privileges.<br><br>
For more details, see the [`download-url`](https://pve.proxmox.com/pve-docs/api-viewer/index.html#/nodes/{node}/storage/{storage}/download-url) API documentation under the "Required permissions" section.

## Example Usage

```terraform
resource "proxmox_virtual_environment_download_file" "release_20231228_debian_12_bookworm_qcow2_img" {
  content_type       = "iso"
  datastore_id       = "local"
  file_name          = "debian-12-generic-amd64-20231228-1609.img"
  node_name          = "pve"
  url                = "https://cloud.debian.org/images/cloud/bookworm/20231228-1609/debian-12-generic-amd64-20231228-1609.qcow2"
  checksum           = "d2fbcf11fb28795842e91364d8c7b69f1870db09ff299eb94e4fbbfa510eb78d141e74c1f4bf6dfa0b7e33d0c3b66e6751886feadb4e9916f778bab1776bdf1b"
  checksum_algorithm = "sha512"
}

resource "proxmox_virtual_environment_download_file" "latest_debian_12_bookworm_qcow2_img" {
  content_type = "iso"
  datastore_id = "local"
  file_name    = "debian-12-generic-amd64.qcow2.img"
  node_name    = "pve"
  url          = "https://cloud.debian.org/images/cloud/bookworm/latest/debian-12-generic-amd64.qcow2"
}

resource "proxmox_virtual_environment_download_file" "latest_ubuntu_22_jammy_qcow2_img" {
  content_type = "iso"
  datastore_id = "local"
  node_name    = "pve"
  url          = "https://cloud-images.ubuntu.com/jammy/current/jammy-server-cloudimg-amd64.img"
}

resource "proxmox_virtual_environment_download_file" "latest_static_ubuntu_24_noble_qcow2_img" {
  content_type = "iso"
  datastore_id = "local"
  node_name    = "pve"
  url          = "https://cloud-images.ubuntu.com/noble/current/noble-server-cloudimg-amd64.img"
  overwrite    = false
}

resource "proxmox_virtual_environment_download_file" "release_20231211_ubuntu_22_jammy_lxc_img" {
  content_type       = "vztmpl"
  datastore_id       = "local"
  node_name          = "pve"
  url                = "https://cloud-images.ubuntu.com/releases/22.04/release-20231211/ubuntu-22.04-server-cloudimg-amd64-root.tar.xz"
  checksum           = "c9997dcfea5d826fd04871f960c513665f2e87dd7450bba99f68a97e60e4586e"
  checksum_algorithm = "sha256"
  upload_timeout     = 4444
}

resource "proxmox_virtual_environment_download_file" "latest_ubuntu_22_jammy_lxc_img" {
  content_type = "vztmpl"
  datastore_id = "local"
  node_name    = "pve"
  url          = "https://cloud-images.ubuntu.com/jammy/current/jammy-server-cloudimg-amd64.tar.gz"
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `content_type` (String) The file content type. Must be `iso` for VM images or `vztmpl` for LXC images.
- `datastore_id` (String) The identifier for the target datastore.
- `node_name` (String) The node name.
- `url` (String) The URL to download the file from. Must match regex: `https?://.*`.

### Optional

- `checksum` (String) The expected checksum of the file.
- `checksum_algorithm` (String) The algorithm to calculate the checksum of the file. Must be `md5` | `sha1` | `sha224` | `sha256` | `sha384` | `sha512`.
- `decompression_algorithm` (String) Decompress the downloaded file using the specified compression algorithm. Must be one of `gz` | `lzo` | `zst` | `bz2`.
- `file_name` (String) The file name. If not provided, it is calculated using `url`. PVE will raise 'wrong file extension' error for some popular extensions file `.raw` or `.qcow2`. Workaround is to use e.g. `.img` instead.
- `overwrite` (Boolean) If `true` and size of uploaded file is different, than size from `url` Content-Length header, file will be downloaded again. If `false`, there will be no checks.
- `overwrite_unmanaged` (Boolean) If `true` and a file with the same name already exists in the datastore, it will be deleted and the new file will be downloaded. If `false` and the file already exists, an error will be returned.
- `upload_timeout` (Number) The file download timeout seconds. Default is 600 (10min).
- `verify` (Boolean) By default `true`. If `false`, no SSL/TLS certificates will be verified.

### Read-Only

- `id` (String) The unique identifier of this resource.
- `size` (Number) The file size.
