
# Unikraft 빌드 및 실행 방법


## 빌드 방법
### Dependency Graph
![plot](./pictures/dependency_graph.PNG)






## 실행 방법

Server와 연결할 Bridge 추가

```
sudo brctl addbr br0
sudo ip a a 172.44.0.1/24 dev br0
sudo ip l set dev br0 u
```

QEMU + Unikraft Image 실행

```
sudo qemu-system-aarch64 -fsdev local,id=myid,path=$(pwd)/fs0,security_model=none \
 -device virtio-9p-pci,fsdev=myid,mount_tag=rootfs,disablemodern=on,disable-legacy=off \
 -netdev bridge,id=en0,br=br0 \
 -device virtio-net-pci,netdev=en0 \
 -kernel "build/app-redis_kvm-arm64" \
 -append "netdev.ipv4_addr=172.44.0.2 netdev.ipv4_gw_addr=172.44.0.1 netdev.ipv4_subnet_mask=255.255.255.0 -- /redis.conf" \
 -machine virt \
 -cpu host \
 --enable-kvm \
 -nographic
```

```
sudo qemu-system-aarch64 -fsdev local,id=myid,path=$(pwd)/fs0,security_model=none \
 -device virtio-9p-pci,fsdev=myid,mount_tag=rootfs,disablemodern=on,disable-legacy=off \
 -netdev bridge,id=en0,br=br0 \
 -device virtio-net-pci,netdev=en0 \
 -kernel "build/app-redis_kvm-arm64" \
 -append "netdev.ipv4_addr=172.44.0.2 netdev.ipv4_gw_addr=172.44.0.1 netdev.ipv4_subnet_mask=255.255.255.0 -- /redis.conf" \
 -machine virt \
 -cpu host \
 --enable-kvm \
 -nographic
```




참고자료: https://github.com/mariasfiraiala/scs-work/blob/master/unikraft-scs/unikraft-scs-for-complex-apps.md
