# Other gateway configuration

We want the gateway to be able to route traffic between VPN clients, so we need to tell the
kernel that this is what we want.

/etc/sysctl.d/99-wireguard-route.conf:

```
net.ipv6.conf.all.forwarding=1
```
