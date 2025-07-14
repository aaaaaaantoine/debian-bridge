## Créer un Brdige permanent avec "systend-netword"

Objectif :

* Créer une configuration bridge parmanente.
* Faire en sorte que les machines virtuelles deviennent accessible depuis le réseau local (et/ou depuis l'extérieur).
* Testé sur Debian 12 et 13


1) Si vous utilisez un gestionnaire de réseau tel que Network Manager, désactiver le.
```sh
sudo systemctl disable --now NetworkManager
# ou
sudo systemctl disable --now netwoking
```

2) Lancez le service systemd:
```sh
sudo systemctl enable systemd-networkd
sudo systemctl start systemd-networkd
```

3) Fichiers de configuration:

```sh
# nano /etc/systemd/network/10-br0.netdev

[NetDev]
Name=br0
Kind=bridge
```
```sh
# nano /etc/systemd/network/10-br0.network

[Match]
Name=br0

[Network]
Address=192.168.1.50/24
Gateway=192.168.1.1
DNS=192.168.1.1
```
```sh
#nano /etc/systemd/network/20-eth0.network
[Match]
Name=enp1s0 #C'est le nom donné lors de la commande "ip a" à modifier si différent.

[Network]
Bridge=br0
```

4) En fin, redémarrez le service:

```sh
sudo systemctl restart systemd-networkd
```

5) Vérifiez que la configuration fonctionne bien
```sh
networkctl status
```
