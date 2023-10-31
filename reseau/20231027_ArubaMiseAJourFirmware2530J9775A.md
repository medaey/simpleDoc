---
layout: post
title: Mise à jour firmware Aruba 2530-J9775A
parent: reseau
---
# Comment mettre à jour le firmware d’un switch Aruba 2530-J9775A ?

⚠️Mettre à jour uniquement images qui n'est actuelement pas utiliser `primary` ou `secondary`. Cela permet de redémarrer sur image non mise à jour en cas de dysfonctionnement.⚠️

## I Vérifier quelle image & quelle version du firmware est utilisé.
```
# Afficher les images présentes sur le commutateur
sh flash
# Vérifier image et la version du firmware actuellement utilisé
sh ver
```

## II Récuperer la dernier version du firwmare sur le site HPE Aruba
![localImage](/assets/images/20231027_HpeArubaSearchFirmware.png)
ℹ️ _Pour se connecter il vous faudra crée un compte.
- [https://asp.arubanetworks.com/downloads;search=ya;sort=VERSION_DESC;fileTypes=SOFTWARE;products=Aruba%20Switches](https://asp.arubanetworks.com/downloads;search=ya;sort=VERSION_DESC;fileTypes=SOFTWARE;products=Aruba%20Switches)

## III Se connecter a la mire web du switch
⚠️Pour accéder à la mire web, assurez-vous que les deux machines peuvent communiquer via IP.⚠️

Si ce n'est pas le cas, branchez votre ordinateur via un câble Ethernet sur le port 1 du switch et attribuez à ordinateur une adresse IP statique du même réseau que le switch.

Afficher adresse IP du switch
```
sh ip
```
Afficher les VLAN
```
sh vlan
```
Mode activé
```
en
```
Mode configuration
```
conf t
```
Passer le port 1 dans le VLAN par default
```
vlan 1 tagged 1
```
Activer la mire web
```
web-management
```
## IV Téléverser le nouveau firmware via la mire web

`Dashboard` > `System` > `FirmwareUpdate`
![localImage](/assets/images/20231027_ArubaWebInterfaceUpdateFirmware.png)
Téléverser la dernier version du firmware sur image non utiliser par le switch cela prend plusieur minutes.

## V Redemarrer le switch sur image qui vient étre mise a jour 
```
# Démarrez le switch en utilisant image primaire 
boot system flash primary
# Démarrez le switch en utilisant image secondaire 
boot system flash secondary
```

# VI Vérifier image et la version du firmware actuellement utilisé
```
sh ver
```

## VII Désactiver la mire web
```
no web-management
```

sources:
- https://www.it-connect.fr/comment-mettre-a-jour-le-firmware-dun-switch-aruba/
- https://cossu.tech/firmwareAruba
- https://techhub.hpe.com/eginfolib/networking/docs/switches/common/15-18/5998-8158_bog/content/ch04s07.html