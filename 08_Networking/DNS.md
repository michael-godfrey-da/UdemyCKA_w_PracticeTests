# DNS


/etc/hosts
```
<ip> <hostname> <alias1> <alias2> ...
```

/etc/resolv.conf
```
# To set the DNS server (can have multiple):
nameserver <ip>

# To set the search domain (allows lookup by subdomain):
search <domain> 
```

To set lookup order:
/etc/nsswitch.conf
``` 
hosts: files dns
```

Record Types:
* A: Address
* AAAA: IPv6 Address
* CNAME: Canonical Name
* MX: Mail Exchange
* NS: Name Server
* PTR: Pointer
* SOA: Start of Authority
* SRV: Service
* TXT: Text

To query DNS:
``` bash
nslookup <domain> <dns server>
```

dig <domain> <record type>
```

To set up a DNS server:

(use CoreDNS)