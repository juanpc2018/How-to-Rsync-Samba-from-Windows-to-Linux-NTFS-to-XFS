# How-to-Rsync-Samba-from-Windows-to-Linux-NTFS-to-XFS

There are many tutorials on the Net,
but None works exactly for Kubuntu.
there are pieces here & there...
others are misleading / decoys.

Samba4.2
Requires winbind
Not installed by default in Kubuntu 21.10 , install with synaptic, muon or similar package manager.

Share the Windows Folder or Drive in Windows,
Select a Proper User & Password,
Giving Full Rights to Everybody does Not work for Samba.

In Linux:
LuckyBackup is a GUI FrontEnd for Rsync, the advantage is that can store different settings / configurations.
similar to AllWaySync for Windows.
but...
Rsync only does ssh over Network, and you want Samba.
"Easy"
after creating a Windows Share in Dolphin / Nautilus, and testing the Windows Drive / Folder is working in Nautilus / Dolphin.
then
you need to mount the SMB shared folder, to a folder Nautilus / Dolphin can detect as Local,
$ mkdir /media/UserName/cifs

but ¿what the hell is cifs?
in FreeBSD is called smbfs
but in Debian is cifs "totally unrelated name"

you can see all the FileSysytems your kernel supports:
$ ls /lib/modules/$(uname -r)/kernel/fs

as recomended by:
$ man mount

there is No smbfs in Debian
but cifs is the same, with a weird name.
+1 point to FreeBSD,
-1 point for Kubuntu
Common Internet File System (CIFS)

$ mount -t cifs /sourceIP/FolderOrDrive /local_destination

Samba requires Login & Password.
minimum User,
some passwords do Not work, if start with a character different than letters or numbers.

$ mount -t cifs -o username=USERNAME,password=PWD //192.168.xxx.xxx/SharedDriveOrFolder /media/user/cifs

if Password is Not compatible:

$ mount -t cifs -o username=USERNAME //192.168.xxx.xxx/SharedDriveOrFolder /media/user/cifs

Samba will ask the password in Konsole,

If the Windows Machine has Static IP on the Router / Network Card,
IF Not, use the Windows Machine Name in System. 

the Network Drive/Folder will appear automatically in Dolphin / Nautilus as Local Linux drive.
with Perfect NTFS compatibility, 

then LuckyBackup can be used as usual, 
with Perfect XFS compatibility.

Large 18TB HSMR HDDs can R&W at 250MB/s
but 1GbE Network = 1000Mbps = 125MB/s.
To avoid Network bottlenecks, needs a faster Network adapter.

SFP+ is 10G
Lc-Lc Om1 Om2 Om3 Fiber Optic cable at 850nm wavelenght for Short Range: 30mts, 80mts, 300mts.
cable is color coded, usually Orange for SR.

SFP is 8G or less, down to 1.25GbE.

There are Faster Network adapters, 
SFP28 = 25GbE, QSFP+ = 40Gbe,
up to 800Gbe.

Problems solved:
#1. Samba4.2 requires winbind
#2. Windows requires to Activate SMB2 & SMB3 and disable SMB1 in PowerShell.
#3. Windows shared Folder / Drive requires proper user & password.
#4. Windows SMB shared Folder / Drive, link needs to be Created in Dolphin Network.
#5. Windows SMB shared Folder / Drive needs to be mounted as local drive in Linux.
#6. then luckyBackup / Rsync will work as usual.
#7. Rsync only works with ssh in Network, No direct SMB.
#8. $ ls smb:// does Not work with SMB shares, SMB shares can only be RW with Dolphin / Nautilus.
#9. $ ls remote:// does Not work with SMB shares, SMB shares can only be RW with Dolphin / Nautilus.
#10. smbclient does Not work with Windows without winbind & reboot.
#11. smbclient is useless for Rsync.
#12. remote://ip4 is useless for Rsync.
#13. smb://ip4 is useless for Rsync.

DONE.

Option B)
Buy Linux NTFS drivers from Paragon
mount the NTFS HDD directly in Linux machine,
problem:
using Free Linux NTFS-3G drivers,
compatibility is Not 100% with large drives 18TB / 20TB.
Rsync will have problems when doing NTFS to XFS.
XFS is the Recomended File Format for Large/Big Mechanical Drives.
Ext4 is Not Recomended for Large/Big Mechanical Drives.

Problem is compatibility between:
Windows, Linux & OSX.

XFS is very good, but Only for Linux,
OSX and Windows have limited Read Only drivers from Paragon and FUSEOSX.

Free HFS+ driver for Linux is very limited / incomplete.
Free NTFS driver for Linux is better than HFS+ but Not 100%.
drivers break very easy with large drives.

NTFS requires constant defrag,
does Not allow ? and many other characters.
its very limited.
thats why Windows Server has ReFS Not NTFS.

Paragon has APFS drivers for Windows & Linux.
OSX has APFS support since OSX HighSierra 10.13.6

That could be the Only File System that is compatible with All systems.
but how does work with Large/Big Mechanical HDDs ? Unknown.

exFAT is free, comtabile between all systems,
but is a very inferior File System vs. others.
Emergency Only type.

If Paragon had full support for XFS in OSX and Windows,
that would be my to go FS.
