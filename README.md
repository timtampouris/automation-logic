# terraform-hetzner
Create a cloud instance on Hetzner Cloud with Floating IP

```
# Create a server
# Various options:
# server_type = "cx21"
# server_type = "cx21-ceph"
# server_type = "cx31"
# server_type = "cx31-ceph"
# server_type = "cx41"
# server_type = "cx51"
# server_type = "ccx11" dedicated cpu
# server_type = "ccx21" dedicated cpu
# datacenter  = "hel1-dc2"
# location    = "hel1"
# datacenter  = "nbg1-dc3"
# location    = "nbg1"
# datacenter  = "fsn1-dc8"
# datacenter  = "fsn1-dc14"
# location    = "fsn1"
# iso         = "CentOS-7-x86_64-NetInstall-1708.iso" Name of the mounted ISO image
# image       = "ubuntu-18.04"

# Provides a Hetzner Cloud Floating IP Assignment to assign a Floating IP
# to a Hetzner Cloud Server. Deleting a Floating IP Assignment will
# unassign the Floating IP from the Server.
resource "hcloud_floating_ip_assignment" "main" {
  floating_ip_id = "${hcloud_floating_ip.master.id}"
  server_id = "${hcloud_server.webtest.id}"
}

resource "hcloud_server" "webtest" {
  name        = "webtest"
  image       = "centos-7"
  server_type = "cx11"
  keep_disk   = "true"
  datacenter  = "hel1-dc2"
  location    = "hel1"
}

# Provides a Hetzner Cloud Floating IP to represent
# a publicly-accessible static IP addresses that
# can be mapped to one of your Servers
resource "hcloud_floating_ip" "master" {
  type      = "ipv4"
  server_id = "${hcloud_server.webtest.id}"
}
```
