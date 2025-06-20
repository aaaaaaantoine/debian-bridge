## Connexion par pont avec Netctl 

* Prérequis :
```sh
sudo apt install -y  bridge-utils netctl
```

```sh
sudo systemctl disable --now NetworkManager
sudo systemctl disable --now netwoking

sudo nano /etc/netctl/bridge

Description="Bridge connection"
Interface=br0
Connection=bridge
BindsToInterfaces=(enp1s0)
MACAddress='52:54:00:a8:b9:6b'
IP=static
Address='192.168.1.31/24'
Gateway='192.168.1.1'
SkipForwardingDelay=yes
```

```sh
sudo netctl enable bridge
sudo netctl start bridge
```
