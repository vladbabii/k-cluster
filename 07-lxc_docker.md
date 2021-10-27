
Reference: https://docs.docker.com/engine/install/ubuntu/


```
apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
    
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null


echo "{ \"registry-mirrors\": [\"http://10.11.9.197:5000\"] }" > /etc/docker/daemon.json

apt-get update

apt-get install -y docker-ce docker-ce-cli containerd.io docker-compose

systemctl status docker
```


