```sh
sudo apt install bridge-utils
```

```sh
sudo brctl addbr br0
sudo brctl addif br0 enp1s0
sudo ifup br0
```

```sh
vim /etc/network/interfaces
auto lo
iface lo inet loopback

allow-hotplug enp1s0

auto br0
    iface br0 inet static
    hwaddress ether 12:34:45:78:90:10
    address 192.168.1.20
    netmask 255.255.255.0
    network 192.168.1.1
    gateway 192.168.1.1
    bridge_ports enp1s0
    bridge_stp off
    bridge_fd 0
```
```sh
sudo systemctl restart networking# debian-bridge
```
