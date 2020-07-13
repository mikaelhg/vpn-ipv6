# What and why

The objective is to set up a IPv6-only "corporate intranet" type VPN,
with services such as secure DNS and NAT64.

IPv6 because I've seen various disasters relating to IPv4 corporate networks
operating in the `10.x.x.x` and `192.168.x.x` spaces.

## Network space

[Private IPv6 space, RFC-4193.](https://tools.ietf.org/html/rfc4193)

```plantuml format="svg" classes="uml myDiagram" alt="My super diagram placeholder" title="My super diagram"
  Goofy ->  MickeyMouse: calls
  Goofy <-- MickeyMouse: responds
```

```plantuml format="svg_inline" classes="uml myDiagram" alt="My super diagram placeholder" title="My super diagram"
  Goofy ->  MickeyMouse: calls
  Goofy <-- MickeyMouse: responds
```

## Local development

[Vagrant](https://www.vagrantup.com/),
[Virtualbox](https://packages.ubuntu.com/focal/virtualbox),
[Ansible](https://www.ansible.com/).

Vagrant and Virtualbox manage local VMs, Ansible provisions them.

Boxes:

* [ubuntu/focal64](https://app.vagrantup.com/ubuntu/boxes/focal64)
* [gusztavvargadr/windows-10](https://app.vagrantup.com/gusztavvargadr/boxes/windows-10)

## VPN tools

[WireGuard](https://www.wireguard.com/), 
[ShadowSocks](https://shadowsocks.org/), 
[TAYGA](http://www.litech.org/tayga/).

WireGuard connects VPN clients and VPN servers.

ShadowSocks provides a TCP 443 connection for WireGuard.

TAYGA provides NAT64 services for connections from the VPN to the outside world.
