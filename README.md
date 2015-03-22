# Mallard

Manage your flock of containers.

## Basic idea

* The system is self contained w/o no need of external commands.
* Ansible is used to setup the remote systems.
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

### etcd

etcd is a clustered key/value storage. It runs inside a docker container on every 
host and is exposed to the user at `172.17.42.1:4001`. It uses the management network 
to talk to the other peers.
