---
layout: post
title: Comment crée un server ipxe compatible uefi
parent: linux
grand_parent: system
---
[Installation d'un serveur PXE sur Debian](https://blog.foulquier.info/tutoriels/systeme/installation-d-un-serveur-pxe-sur-debian)

[PXE avec support EFI](https://forum-debian.fr/wiki/PXE_avec_support_EFI)

[Code Architecture iPXE](https://ipxe.org/cfg/platform)

[Projet netboot.xyz](https://github.com/netbootxyz/netboot.xyz)

```bash
if  exists ipxe.http
    and exists ipxe.menu
    and exists ipxe.iSCSI
{
    filename "http://192.168.1.10/boot.ipxe";
} else if option arch = 00:06 {
      filename "ipxe-x86.efi";
} else if option arch = 00:07 {
      filename "ipxe-x64.efi";
} else if option arch = 00:09 {
      filename "ipxe-x64.efi";
} else {
      filename "ipxe.pxe";
}
```

[Signature des firmware pour le secure boot](https://ipxe.org/appnote/etoken#creating_a_uefi_signing_submission)
