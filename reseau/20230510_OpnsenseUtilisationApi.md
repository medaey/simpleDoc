---
layout: post
title: Utilisation api opnsense
parent: reseau
---
Documentation :
 [Utiliser API OPNsense](https://docs.opnsense.org/development/api.html#introduction)
[Configuration des VLAN Opensense](https://techexpert.tips/fr/opnsense-fr/opnsense-vlan-configuration/)


## Mise en place et utilisation
Prérequis pour pouvoir utiliser l'api OPNsense : 

- [ ] Le protocole HTTPS doit être actif sur la mire web d'administration.
   `System > Settings > Administration`
   
- [ ] Avoir une clés d'accès api et son secret.
   `System > Access > Users > Edit > API keys`

*ℹ️ Utiliser votre navigateur web pour voir les appel api F12 > Network > Cliquer sur un éléments de la liste*

## GET

*Voici un exemple de requête sur l'api OPNsense avec la Méthode **GET** pour récupérer des information via la commande curl .*

```bash
# Ajout clef secret et ip dans des variable
key="Cn2qmZ1DFzAXsm/VaxNHy8Omn46wH647qUEFBCeBdYPxerPEjGM1YjRXYrevJoW/BK3IJErQQYSN/t1M"
secret="7mLGto3mcjzWTogffnLGhSIAqjtNSVJJdZKvjcl5B/ZRd729uteoTKcVs4rrul0C+wsbae1ar8BxyO5Z"
ip="192.168.1.188"

# Récupére des information sur le firmware
curl -k -u "$key":"$secret" https://$ip/api/core/firmware/status 2>/dev/null | jq
```
### Exemple d'utilisation de l'api dans ansible
```yaml
- name: Get firmware status from API
  uri:
    url: "https://192.168.1.188/api/core/firmware/status"
    method: GET
    validate_certs: no
    user: "EltQJ/DI8uby96ZmdOVL3EHGFclJr2FkEJw5E+4yuqIajtjnMZXK3ocCrsj6PZKCsouZu94jfX7upICE"
    password: "7YnzoxuspWfQjtoyIT+pCjJ9g3M8ov65Na8KJFDcPAl5AaxNudz6/wTGV6cMa/p7lAINFvM4MSKDLDY/"
  register: firmware_status

- name: Display firmware version
  debug:
    var: firmware_status.json | json_query('version')
```
## POST

#### Vérifier si il y a des mise a jour a faire

```bash
curl -k -u "$key":"$secret" https://$ip/api/core/firmware/status 2>/dev/null | jq '{status_msg}'
```
#### Mettre a jour le firmware

```json
curl -XPOST -d "{\"upgrade\":\"all\"}" -H "Content-Type: application/json" -k -u "$key":"$secret" https://$ip/api/core/firmware/update 2>/dev/null | jq
```
*⚠️ La machine va redémarré pour appliquer les mise a jour ⚠️*

#### Vérifier l'avancement de la mise a jour du firmware + mise en forme du texte de sortie

```bash
curl -XPOST -d "{\"upgrade\":\"all\"}" -H "Content-Type: application/json" -k -u "$key":"$secret" https://$ip/api/core/firmware/upgradestatus 2>/dev/null | jq --raw-output '.log | @text'
``` 
