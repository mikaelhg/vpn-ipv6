# IPv6-only VPN... with NAT into the IPv4 world

https://stanislas.blog/2019/01/how-to-setup-vpn-server-wireguard-nat-ipv6/

https://www.tachyondynamics.com/2019/11/24/ipv6-only-your-network-cheap-and-easy/

https://rtodto.net/how-do-nat64-and-dns64-work-in-ipv6-world-and-srx-config/

http://www.litech.org/tayga/

https://developers.google.com/speed/public-dns/docs/dns64

## Documentation

Develop the documentation locally with:

```
docker run --rm -it -p 8000:8000 -v ${PWD}:/docs mikaelhg/mkdocs-material-plantuml

docker run --rm -it -u 1000 -p 8000:8000 -v ${PWD}:/docs:ro \
    mikaelhg/mkdocs-material-plantuml serve -a 0.0.0.0:8000
```
