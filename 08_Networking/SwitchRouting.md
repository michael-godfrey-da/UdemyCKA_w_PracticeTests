
To see host interfaces:
``` bash
ip link
```

To enable or disable an interface:
``` bash
ip link set dev eth0 up
ip link set dev eth0 down
``` 

To set an IP address (on the host machine):
``` bash
ip addr add 192.168.1.10/24 dev eth0
```

To display routing table:
``` bash
route
```
To Configure a Gateway:
``` bash
# Add a route to the 192.168.2.x network via the gateway at 192.168.1.1
ip route add 192.168.2.0/24 via 192.168.1.1

# Add a route to any unknown address via the gateway at 192.168.1.1
ip route add default via 192.168.1.1
```


To allow forwarding between network interfaces:
``` bash
echo 1 > /proc/sys/net/ipv4/ip_forward
```

To make this permanent, add the following line to /etc/sysctl.conf:
``` bash
net.ipv4.ip_forward = 1
```
