---
layout: post
title: Cette copie de Windows n'est pas authentique
parent: 2022
---

Vous avez cette erreur alors que vous posséder une version originale de Windows?  
Les 2 commandes ci-dessous devraient résoudre ce problème.  

**1)** Ouvrir une invitation de commandes en tant qu'administrateur  
![](https://1.bp.blogspot.com/-JBaNCPNeyyQ/YLVrX1gy7LI/AAAAAAAAE9k/6OwGki9dSkU02qwYa2OZzSZVvNr6zy0rwCPcBGAYYCw/s16000/oem_1.webp)

**2)** Réinitialise les licences avec cette commande:
```batch
slmgr /rilc
```
 _(Cette commande réinitialise toutes les licences stockées dans les dossiers_  
_**%SystemRoot%\system32\oem** et **%SystemRoot%\System32\spp\tokens**)_  

**3)** Réinitialise les minuteurs d'activation:
```batch
slmgr /rearm
```
Si l'erreur **0xc004D307** apparaît faite les étapes **4\*,5\*,6\*** sinon passer à l'étape **7**

![](https://4.bp.blogspot.com/-G-5XCmbmOWg/WlymAOkZVHI/AAAAAAAAAJs/ucOx-EsYTzAfEMev6Wn-UZi4O93YGdMUgCLcBGAs/s1600/erreur_0XC004D307.jpg)


**4\*)** Lancer l'éditeur de registre Windows + R tapez **regedit**
 **![](https://1.bp.blogspot.com/-iiuH5nyVtUI/YLQkEGsi8JI/AAAAAAAAE7o/ScFdiocYNkoKmH4aEsbdUdRoFbrptqLkwCPcBGAYYCw/s16000/ezgif.com-gif-maker%25281%2529.gif)**  

**5\*)** Modifier la clef de registre **SkipRearm** (suivre le chemin ci-dessous):  
```regedit
HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SoftwareProtectionPlatform
```

**6\*)** Modifier la valeur de **SkipRearm** de 0 à 1.
![](https://1.bp.blogspot.com/-9bwdFxCUABM/YLV7CN1EG9I/AAAAAAAAE_c/ydtXJu5d6Js0Gg1ggGX4rtAy7Nlc31b8gCNcBGAsYHQ/s16000/a4cfa-iss7t.webp)

Cette fois-ci la commande de l'étape **3** devrait fonctionner  
```batch
slmgr /rearm
```
**7) Redémarrer** l'ordinateur  

**8)** Vérifier que la licence Windows est bien activée Windows + R tapez **slui**
**
![](https://1.bp.blogspot.com/-K9lLhJ0LYdc/YLV51fJ2RWI/AAAAAAAAE_M/cedetBB8kZkxVN3QdEjJZxBTZ3xtwmAzQCNcBGAsYHQ/s16000/aomgb-dz8xt.webp)
**

_**Windows 7:**_
 _**![](https://1.bp.blogspot.com/-eAn2LxIjJBU/YLV5Lp9E2lI/AAAAAAAAE_E/BSfjcq4nq90cnZ7fg9688M3IeLuTVvgZwCNcBGAsYHQ/s16000/Activation-r%25C3%25A9ussie.webp)**_  

**_Windows 10:_**
 **_![](https://1.bp.blogspot.com/-NOKruhSPBTM/YLV56YJo3xI/AAAAAAAAE_Q/-wf6K974-EA1iWBkPOxPwnZKVs1BJdLuACNcBGAsYHQ/s16000/aazpp-focc6.webp)_**  

**[microsoft.com](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn502540(v=ws.11))**
