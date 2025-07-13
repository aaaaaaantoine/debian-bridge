## Connexion par pont avec Netctl 

Objectif :

* Faire en sorte que les machines virtuelles deviennent accessible depuis le réseau local (ou depuis l'extérieur).
* Testé uniquement sur Debian 13 Trixie

* Prérequis :
```sh
curl -O http://ftp.fr.debian.org/debian/pool/main/n/netctl/netctl_1.29-1_all.deb
sudo apt install netctl_1.29-1_all.deb
```

* Si vous utilisez un gestionnaire de réseau tel que Network Manager, désactiver le.
```sh
sudo systemctl disable --now NetworkManager
# ou
sudo systemctl disable --now netwoking
```

* Fichier de configuration, s'il n'existe pas, créez le.
```sh

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

* En fin, démarrez votre pont ici 'bridge'.

```sh
sudo netctl enable bridge
sudo netctl start bridge
```
