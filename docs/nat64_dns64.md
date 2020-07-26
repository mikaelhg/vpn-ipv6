# NAT64 and DNS64

Let's say that your mobile phone is in a IPv6-only network, only has an IPv6
address and IPv6 routing. But you want to connect to some random web service
which only has an IPv4 address. How does this work?

Well, in your IPv6-only network, you have a special DNS server which resolves
the queries of your IPv6-only devices, such as your mobile phone.

When you type "www.example.com" in your browser, (and unbeknownst to you,
behind the scenes "www.example.com" only has the IPv4 address 1.2.3.4,)
your browser takes that name, and makes a DNS query to first resolve it
into a IP address.

In our IPv6-only network, we have a special DNS64 proxy, which forwards
that query to your ISP's normal DNS server, which responds with 1.2.3.4.

However, your special DNS64 proxy now takes the 1.2.3.4 and appends it
to a IPv6 address prefix which you've set up for this purpose.

Let's say, we translate 1.2.3.4 to XXXX:XXXX:XXXX:XXXX:0102:0304 this way.

Now your browser thinks that "www.example.com" is located at the IPv6
address XXXX:XXXX:XXXX:XXXX:0102:0304, and therefore tries to open a TCPv6
connection to that IP, port 443 as usual.

The other part of this equation is a special NAT64 gateway, which sits between 
the IPv6 world and the IPv4 world, and can transform a IPv6 packet destinied
to XXXX:XXXX:XXXX:XXXX:0102:0304 into a IPv4 packet destinied to 1.2.3.4,
as well as perform the usual NAT tricks.

You have to set up your network to route all packets which come from your
IPv6-only local devices such as your mobile phone, and which are destinied 
to any XXXX:XXXX:XXXX:XXXX:: address, through that NAT64 gateway.

This way, the NAT64 gateway translates packet addresses from IPv6 to IPv4, 
and from IPv4 to IPv6, using the address spaces which you've reserved for
this use, as well as keep track of every TCP connection which has been 
opened from the IPv6 side to the IPv4 side. 

I don't know how UDP is handled, as it's stateless.

## CoreDNS for DNS64

It looks like the by far easiest way to implement DNS64 as well as an
VPN-internal name server, will be to use CoreDNS, and install it with
Ansible from their GitHub binary releases.

The CoreDNS configuration format seems pretty simple.

/etc/Corefile

```
poc.vpn {
  bind fd8d:407b:d075:8a7e::1
  hosts poc.vpn.hosts
  log
}

. {
  bind fd8d:407b:d075:8a7e::1
  forward . 8.8.8.8
  log
}
```

/etc/poc.vpn.hosts

```
fd8d:407b:d075:8a7e::1  gateway.poc.vpn
fd8d:407b:d075:8a7e::5  home1.poc.vpn
```
