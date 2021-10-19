## install keepalived
```
apt install -y keepalived
```

## edit /etc/keepalived/keepalived.conf
```
vrrp_script chk_service {
    script "/usr/bin/pkill -o lighttpd"
    interval 2
    weight 2
}

vrrp_instance VI_1 {
    interface eth0
    state MASTER
    nopreempt
    interface eth0
    priority 200

    virtual_router_id 33
    unicast_src_ip <node ip>
    unicast_peer {
        <node 2 ip>
        <node 3 ip>
    }

    authentication {
        auth_type PASS
        auth_pass helowlcm
    }

    track_script {
        chk_service
    }

    virtual_ipaddress {
      <floating ip>
    }
#    notify_master /etc/keepalived/master.sh
}
```

## restart keepalived
```
systemctl restart keepalived
systemctl status keepalived
```

