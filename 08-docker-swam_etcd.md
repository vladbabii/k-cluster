```
docker network create -d overlay --attachable etcd
```

```
version: '2'

services:
  etcd1:
    image: docker.io/bitnami/etcd:3
    environment:
      - ALLOW_NONE_AUTHENTICATION=yes
      - ETCD_NAME=etcd01
      - ETCD_INITIAL_ADVERTISE_PEER_URLS=http://10.99.101.2:2380
      - ETCD_LISTEN_PEER_URLS=http://0.0.0.0:2380
      - ETCD_ADVERTISE_CLIENT_URLS=http://10.99.101.2:2379
      - ETCD_LISTEN_CLIENT_URLS=http://0.0.0.0:2379
      - ETCD_INITIAL_CLUSTER_TOKEN=etcd-cluster
      - ETCD_INITIAL_CLUSTER=etcd01=http://10.99.101.2:2380,etcd02=http://10.99.102.2:2380,etcd03=http://10.99.103.2:2380
      - ETCD_INITIAL_CLUSTER_STATE=new
    ports:
      - "2380:2380/tcp"
      - "2380:2380/udp"
      - "2379:2379/tcp"
      - "2379:2379/udp"
    volumes:
      - /data/etcd/data:/bitnami/etcd
```
