---
layout: post
title: Mettre a jour serveur rustdesk
parent: linux
grand_parent: system
---

### Fair les mise a jour d'un serveur rustedesk
1 - Téléchager le dernier version des binaire sur [Github](https://github.com/rustdesk/rustdesk-server/releases/latest) en fonction de votre architecture.
```bash
# amd64
wget https://github.com/rustdesk/rustdesk-server/releases/latest/download/rustdesk-server-linux-amd64.zip
```

2 - Décompreser le fichier zip
```bash
unzip rustdesk-server-linux-amd64.zip
```

3 - Vérifier la version des binaires télécharger
```bash
./amd64/hbbr -V
./amd64/hbbs -V
```

4 - Arreter les service hbbr et hbbs via pm2
```bash
pm2 stop hbbr hbbs
```

5 - Démarrer les service hbbs et hbbr
```bash
pm2 start hbbs -- -r helpdesk.gmte77.org:21117 -k _
pm2 start hbbr
```

6 - Vérifier la bonne execution
```bash
pm2 monit
```

### sources
- [Utilisation de pm2](https://pm2.keymetrics.io/)
- [Installation du serveur RustDesk](https://rustdesk.com/docs/en/self-host/install/#step-3--set-hbbshbbr-address-on-client-side)
