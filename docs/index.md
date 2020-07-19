# What and why

The objective is to set up a demonstration IPv6-only "corporate intranet" type VPN,
with services such as secure DNS and NAT64.

IPv6-only, because I've seen various disasters relating to IPv4 corporate networks
operating in the `10.x.x.x` and `192.168.x.x` spaces, which many ISP devices in
people's homes also use... and merging companies using the same spaces...

## How to reproduce the demonstration locally

In the `Vagrantfile`, you can find a description of the virtual machines which are
automatically created by Vagrant for this demonstration, as well as their local IP
addresses, and memory and CPU reservations, which you might want to tweak if necessary.

1. Install VirtualBox and Vagrant

2. `vagrant up`

3. `vagrant ssh home1`, `ping fd8d:407b:d075:8a7e::1` and `sudo wg show`

4. `vagrant ssh gateway`, `ping fd8d:407b:d075:8a7e::5` and `sudo wg show`

## Network space

[Private IPv6 space, RFC-4193.](https://tools.ietf.org/html/rfc4193)

```plantuml format="png"
nwdiag {
  network internet {
      gateway [address = "5.5.5.5"];
      home1 [address = "1.2.3.4"];
      office1 [address = "2.4.1.2"];
  }
  network private {
      address = "fd8d:407b:d075:8a7e::/64";
      gateway [address = "fd8d:407b:d075:8a7e::1"];
      home1 [address = "fd8d:407b:d075:8a7e::5"];
      office1 [address = "fd8d:407b:d075:8a7e::6"];
  }
}
```

### Chosen IPv6 private space

https://www.ultratools.com/tools/rangeGenerator

```
Prefix/L: fd
Global ID: 8d407bd075
Subnet ID: 8a7e
Combine/CID: fd8d:407b:d075:8a7e::/64
IPv6 addresses: fd8d:407b:d075:8a7e::/64:XXXX:XXXX:XXXX:XXXX
Start Range: fd8d:407b:d075:8a7e:0:0:0:0
End Range: fd8d:407b:d075:8a7e:ffff:ffff:ffff:ffff
No. of hosts: 18446744073709551616
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

## Tools to investigate

https://github.com/DNSCrypt/dnscrypt-proxy
