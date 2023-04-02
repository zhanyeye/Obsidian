
那么将对应的网卡启动混淆模式
```sh
sudo ip link set eno1 promisc on
sudo ip link set enx00e04b3a0d01 promisc on
```

为了以防万一，比如外接网卡可能在服务器重启后失效，那么还要加入开机自启动


docker network create -d macvlan -o parent=enx00e04b3a0d01 macnet2

```sh
docker network create -d macvlan --subnet=192.168.0.0/24 --gateway=192.168.0.1 -o parent=eno1 macnet

```

```sh
docker run -d \
  --name openwrt \
  --network macnet \
  --privileged \
  --restart always \
  sulinggg/openwrt:x86_64 /sbin/init
```

docker run --restart always --name openwrt -d --network macnet --privileged sulinggg/openwrt:x86_64 /sbin/init