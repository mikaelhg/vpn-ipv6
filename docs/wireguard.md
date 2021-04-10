# Wireguard

Of course, these keys aren't actually used anywhere, they're just for this
local demo, and can be found from the actual repo as well.

Keys are generated with the command 

```
wg genkey | tee privatekey | wg pubkey > publickey
```

## `gateway`

/etc/wireguard/wg0.conf:

```conf
[Interface]
PrivateKey = GA7JaXAqjG6xKTzBmhB4c2ggqZazZFZt6ywIA3RW6nQ=
Address = fd8d:407b:d075:8a7e::1/64
ListenPort = 51820

[Peer]
# home1
PublicKey = K+tbD5OWKJeRYGyCFDWigJNieeiz4NRo4Q7BsD+ivwc=
AllowedIPs = fd8d:407b:d075:8a7e::5/128
```

See the difference in the `home1` `AllowedIPs` between the gateway and
the client? On the gateway, we're saying `/128` and on the peer we're
saying `/64`.

Note that you'll have to manually add all of the peers to the gateway, 
if you don't allow automatic adds.

In the Peer section for `home1`, we're explicitly saying that we only
allow traffic from that IP to cross from the VPN link to our direction,
even if the client tried to route traffic from other IPs through the link.

## `home1`

```conf
[Interface]
PrivateKey = WNVoPZ+/OpPmId9x6RnCBWDbQ/vXaNgHpYyITEa9QU8=
Address = fd8d:407b:d075:8a7e::5/64

[Peer]
# gateway
PublicKey = pl1LI/XQpwQfPmzGN7Xclidsr34W9CGVAc4plbzmg0o=
Endpoint = 10.200.1.10:51820
AllowedIPs = fd8d:407b:d075:8a7e::/64
```

So, on the client, we're setting our VPN IP explicitly in the Interface,
and the AllowedIPs in the Peer section means that we allow traffic from
those IPs to cross from the VPN to our machine.
