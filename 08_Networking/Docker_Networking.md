# Docker Networking

```bash

# No networking allowed
docker run --network none nginx

# Share the host's network stack
docker run --network host nginx

```

```bash

# To view networks
docker network ls

# Docker creates three networks by default:
# * bridge: Default network for containers
# * host: Shares the host's network stack
# * none: No networking 

# Bridge is known as the docker0 network on host
ip link show docker0
ip addr show docker0

# Create a new network
docker network create my-network
```
