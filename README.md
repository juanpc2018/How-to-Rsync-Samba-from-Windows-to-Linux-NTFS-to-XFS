# How-to-Rsync-Samba-from-Windows-to-Linux-NTFS-to-XFS

There are many tutorials on the Net,
but None works exactly for Kubuntu.
there are pieces here & there...
others are misleading / decoys.

Samba4.2
Requires winbind
Not installed by default in Kubuntu 21.10
synaptic, muon or similar package manager.

Share the Windows Folder,
Select a Proper User & Password,
Giving Full Rights to Everybody does Not work.

In Linux:
LuckyBackup is a GUI FrontEnd for Rsync, the advantage is that can store different settings / configurations.
similar to AllWaySync for Windows.
but...
Rsync only does ssh over Network.
but you want Samba
"Easy"
after creating a Windows Share in Dolphin / Nautilus, and testing the Windows Shared Drive / Folder is working in Nautilus / Dolphin.
then
you need to mount the SMB shared folder, to a folder Nautilus / Dolphin can detect.
as Local,
$ mkdir /media/UserName/cifs

but ¿what the hell is cifs?
in FreeBSD is called smbfs
but in Debian is cifs "totally unrelated name"

you can see the FS your kernel support:
$ ls /lib/modules/$(uname -r)/kernel/fs

as recomended by:
$ man mount

there is No smbfs
but cifs is the same, with a weird name.
+1 point to FreeBSD,
-1 point for Kubuntu

$ mount -t cifs /source /destination

but Samba requires Login & Password.
minimum User Login
some passwords do Not work, if start with a character different than letters or numbers

$ mount -t cifs -o username=USERNAME,password=PASSWD //192.168.xxx.xxx/SharedDrivreOrFolder /media/user/cifs

if Password is Not compatible:

$ mount -t cifs -o username=USERNAME //192.168.xxx.xxx/SharedDrivreOrFolder /media/user/cifs

then will ask the password in Konsole,

and the Network Drive/Folder will appear in Dolphin / Nautilus as Local

then can be used as usual with luckyBakup.

Problems solved:
#1. Samba4.2 requires winbind
#2. Windows requires to Activate SMB2 & SMB3 and disable SMB1 in PowerShell.
#3. Windows shared Folder / Drive requires proper user & password.
#4. Windows SMB shared Folder / Drive, link needs to be Created in Dolphin Network.
#5. Windows SMB shared Folder / Drive needs to be mounted as local drive in Linux.
$6. then luckyBackup / Rsync will work as usual.
Rsync only works with ssh in Network,
No direct SMB.

DONE.
