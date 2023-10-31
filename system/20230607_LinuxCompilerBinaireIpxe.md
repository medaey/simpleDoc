---
layout: post
title: Compilation des binaire ipxe
parent: linux
grand_parent: system
---
---
# Install compiler and dependencies
```
sudo apt-get install -y git gcc make liblzma-dev
```
# Grab the source code
```
git clone https://github.com/ipxe/ipxe.git
cd ipxe/src
```

# Enable NFS support
```
sed -i 's/#undef\tDOWNLOAD_PROTO_NFS/#define\tDOWNLOAD_PROTO_NFS/' config/general.h
```

# Enable Ping support
```
sed -i 's/\/\/#define\ PING_CMD/#define\ PING_CMD/' config/general.h
sed -i 's/\/\/#define\ IPSTAT_CMD/#define\ IPSTAT_CMD/' config/general.h
sed -i 's/\/\/#define\ REBOOT_CMD/#define\ REBOOT_CMD/' config/general.h
sed -i 's/\/\/#define\ POWEROFF/#define\ POWEROFF/' config/general.h
```

# Create the embedded script for break the loop
nano ipxe/src/embed.ipxe
```
#!ipxe

dhcp
chain tftp://${next-server}/main.ipxe || shell
```

# Compile all IPXE bin
```
make bin/ipxe.pxe
make bin-x86_64-efi/ipxe.efi
make bin-i386-efi/ipxe.efi
make bin/undionly.kpxe EMBED=embed.ipxe
```
# Move all IPXE bin in folder `/tmp/iPXE`
```
mkdir -p /tmp/iPXE
cp bin/ipxe.pxe /tmp/iPXE/ipxe.pxe
cp bin-x86_64-efi/ipxe.efi /tmp/iPXE/ipxe-x64.efi
cp bin-i386-efi/ipxe.efi /tmp/iPXE/ipxe-x86.efi
cp bin/undionly.kpxe /tmp/iPXE/undionly.kpxe
```