---
layout: post
title: Vérifier et réparer l'intégrité du système
parent: windows-client
grand_parent: system
---

# Comment vérifier et réparer un système Windows endommagé
Les commandes ci-dessous permettent de vérifier l'intégrité du système et de le réparer si nécessaire.

⚠️ Cette opération est relativement longue (30min à 2 heures) et s'accompagne de redémarrage si le systéme est endommagé. ⚠️

```powershell
# Vérifie les fichiers système Windows et tente de les réparer.
sfc /scannow
# Vérifie l'intégrité de l'image du système.
Dism /Online /Cleanup-Image /ScanHealth
# Effectue une vérification supplémentaire de l'intégrité de l'image du système.
Dism /Online /Cleanup-Image /CheckHealth
# Tente de réparer des composants du système corrompus.
Dism /Online /Cleanup-Image /RestoreHealth
```