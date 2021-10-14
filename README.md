#!/bin/bash

## Swap Area

```
sudo fallocate -l 2G /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
sudo sysctl vm.swappiness=10
echo 'vm.swappiness=10' | sudo tee -a /etc/sysctl.conf
```

## Applications

```
docker stack deploy -c traefik-compose.yml traefik

docker stack depoy -c api-compose.yml api

cd talk && docker stack deploy -c talk-compose.yml talk && cd ..
cd attack && docker stack deploy -c attack-compose.yml attack && cd ..
cd demo && docker stack deploy -c demo-compose.yml demo && cd ..
cd orca && docker stack deploy -c orca-compose.yml orca && cd ..
cd ros && docker stack deploy -c ros-compose.yml ros && cd ..

mkdir -p ~/linx-data && chmod -R 777 ~/linx-data && docker stack deploy -c linx-compose.yml linx
```

