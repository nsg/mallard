# Mallard

![Mallard](http://i.imgur.com/K11jKCu.jpg)

Manage your flock of containers.

## Basic idea

* The system is self contained w/o no need of external commands and tools.
* Ansible is used to setup the remote systems (or use docker).
* The machines are in a mesh network in a master-master setup.

## Technology

### Tinc VPN

All nods joins a meshed network in the 10.10.0.0/24 range. The VPN is encrypted
and is a secure backend network for services. This network is never exposed to
the internet. Be careful to expose this to untrusted containers.

```
           host0                10.10.0.1
          /  |  \
    host1 ---+--- host2         10.10.0.{2,3}
          \  |  /
           host3                10.10.0.4

```

### Docker

The container manager Docker is installed on all nodes. Docker listens on both the
default unix socket and on the internal VPN.

### Swarm

Docker Swarm is installed on all nodes, both the agent and manager.

### Consul

Consul is installed on all hosts.

### Monit

Monit is used to keep track on processes and (re)start them if needed.
