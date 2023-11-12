# Network Namespaces

To create a namespace:
``` bash
ip netns add <name>

# list namespaces
ip netns
ip netns list

# List interfaces
ip link

# List interfaces in a namespace
ip netns exec <namespace> ip link
ip -n <namespace> link

# To view the routing table in a namespace:
ip netns exec <namespace> route

# Create a veth pair
ip link add <pair-name1> type veth peer name <pair-name2>
ip link set <pair-name1> ns <namespace1>
ip link set <pair-name2> ns <namespace2>
ip -n <namespace1> addr add <gateway-ip1> dev <pair-name1>
ip -n <namespace2> addr add <gateway-ip2> dev <pair-name2>

# To ping from one namespace to another:
ip netns exec <namespace1> ping <gateway-ip2>

# To delete a namespace:
ip netns del <namespace>
```

Virtual Bridge Network:
``` bash
ip link add <bridge-name> type bridge
ip link set <bridge-name> up

# Add an interface to the bridge
ip link set <interface> master <bridge-name>

```
