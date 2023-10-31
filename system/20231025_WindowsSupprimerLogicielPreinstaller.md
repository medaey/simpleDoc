---
layout: post
title: Supprimer les logiciels préinstaller avec powershell
parent: windows-client
grand_parent: system
---
# Windows 10 comment supprimer les logiciels préinstaller avec powershell ?

Lister les application installer sur tout les utilisateur
```powershell
Get-AppxPackage –AllUsers
```

Supprimer des application Xbox
```powershell
Get-AppxPackage -AllUsers *XboxIdentity* | Remove-AppxPackage
Get-AppxPackage -AllUsers *XboxSpeech* | Remove-AppxPackage
Get-AppxPackage -AllUsers *XboxGameOverlay* | Remove-AppxPackage
Get-AppxPackage -AllUsers *XboxApp* | Remove-AppxPackage
```

Supprimer Solitaire
```powershell
Get-AppxPackage -AllUsers *Solit* | Remove-AppxPackage
```

Supprimer de Mobilite Conneté Microsoft
```powershell
Get-AppxPackage -AllUsers *YourPhone* | Remove-AppxPackage
```

Source:
- [ginjfo.com](https://www.ginjfo.com/actualites/logiciels/windows-9/windows-10-comment-supprimer-le-preinstalle-made-in-microsoft-20150810)
