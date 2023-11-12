# Bridge Networking / CNI

Roughly the same process everywhere

1. Create a network namespace
2. Create a bridge network
3. Create a veth pair
4. Add one end of the veth pair to the bridge network
5. Add the other end of the veth pair to the network namespace
6. Assign an IP address to the veth interface in the network namespace
7. Enable IP forwarding on the host
8. Bring up the veth interface in the network namespace
9. Enable NAT (IP masquerading on the host)