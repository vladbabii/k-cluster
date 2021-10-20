```
frontend etcd_frontend
  bind *:2379
  mode tcp
  default_backend etcd_backend

backend etcd_backend
  mode tcp
  server etcd01 10.99.101.2:2379 check        inter 500 fall 3 rise 40
  server etcd02 10.99.102.2:2379 check backup inter 500 fall 3 rise 40
  server etcd03 10.99.103.2:2379 check backup inter 500 fall 3 rise 40


frontend stats
  bind *:1081
  stats enable
  stats uri /
  stats refresh 10s
```
