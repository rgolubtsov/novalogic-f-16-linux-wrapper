# NovaLogic F-16 Multirole Fighter Playable Demo Linux Wrapper

Copy the game distribution's self-extracting InstallShield installation executable from a CD to the hard drive:

```
$ sudo mount /dev/cdrom ./mnt
mount: /home/<username>/mnt: WARNING: device write-protected, mounted read-only.
$
$ mount
...
/dev/sr0 on /home/<username>/mnt type iso9660 (ro,relatime,norock,check=r,map=n,blocksize=2048)
$
$ cp -vR ./mnt/NovaLogic .
'./mnt/NovaLogic' -> './NovaLogic'
'./mnt/NovaLogic/F-16 Multirole Fighter - Single_Multiplayer Demo' -> './NovaLogic/F-16 Multirole Fighter - Single_Multiplayer Demo'
'./mnt/NovaLogic/F-16 Multirole Fighter - Single_Multiplayer Demo/f16demo.exe' -> './NovaLogic/F-16 Multirole Fighter - Single_Multiplayer Demo/f16demo.exe'
$
$ sudo umount ./mnt
$
$ eject
```

Download the `wine` package along with all its necessary dependencies as Pacman proposes to do that, but do not install any of them including Wine itself:

```
$ sudo pacman -Syw wine
:: Synchronizing package databases...
...
resolving dependencies...

Packages (11) faudio-19.07-1  lib32-faudio-19.07-1  lib32-gettext-0.19.8.1-2  lib32-lcms2-2.9-1  lib32-libnl-3.4.0-1
              lib32-libpcap-1.9.0-1  lib32-libusb-1.0.22-1  lib32-libxcursor-1.2.0-1  lib32-libxrandr-1.5.2-1
              lib32-sdl2-2.0.9-1  wine-4.12.1-1

Total Download Size:  51.04 MiB

:: Proceed with download? [Y/n]
...
$
$ ls -al /var/cache/pacman/pkg/wine-4.12.1-1-x86_64.pkg.tar.xz
-rw-r--r-- 1 root root 51468064 Jul 11 23:15 /var/cache/pacman/pkg/wine-4.12.1-1-x86_64.pkg.tar.xz
```

Create a directory where to extract the `wine` package and do extract it there:

```
$ mkdir wine && cd wine && tar -xf /var/cache/pacman/pkg/wine-4.12.1-1-x86_64.pkg.tar.xz
$
$ ls -al
total 336
drwxr-xr-x  4 <username> <usergroup>   4096 Jul 24 19:50 .
drwx------ 45 <username> <usergroup>   4096 Jul 24 19:50 ..
-rw-r--r--  1 <username> <usergroup>  15188 Jul 11 22:34 .BUILDINFO
drwxr-xr-x  3 <username> <usergroup>   4096 Jul 11 22:34 etc
-rw-r--r--  1 <username> <usergroup>    202 Jul 11 22:34 .INSTALL
-rw-r--r--  1 <username> <usergroup> 295365 Jul 11 22:34 .MTREE
-rw-r--r--  1 <username> <usergroup>   4109 Jul 11 22:34 .PKGINFO
drwxr-xr-x  7 <username> <usergroup>   4096 Jul 11 22:34 usr
```

It is possible trying to run the game distribution's self-extracting InstallShield installation executable as is and check it out using the `file` command to make sure it is in fact a Windows PE32 executable:

```
$ ls -al ~/NovaLogic/F-16\ Multirole\ Fighter\ -\ Single_Multiplayer\ Demo/f16demo.exe
-r-xr-xr-x 1 <username> <usergroup> 25469793 Jul 24 19:40 '/home/<username>/NovaLogic/F-16 Multirole Fighter - Single_Multiplayer Demo/f16demo.exe'
$
$ ~/NovaLogic/F-16\ Multirole\ Fighter\ -\ Single_Multiplayer\ Demo/f16demo.exe
bash: /home/<username>/NovaLogic/F-16 Multirole Fighter - Single_Multiplayer Demo/f16demo.exe: cannot execute binary file: Exec format error
$
$ file ~/NovaLogic/F-16\ Multirole\ Fighter\ -\ Single_Multiplayer\ Demo/f16demo.exe
/home/<username>/NovaLogic/F-16 Multirole Fighter - Single_Multiplayer Demo/f16demo.exe: PE32 executable (GUI) Intel 80386, for MS Windows, InstallShield self-extracting archive
```

From now on the use of Wine is required to launch the installation. During launching of Wine it may probably ask to install Wine Mono and Wine Gecko support libraries &ndash; discard them anyway and ignore any errors like the following ones, printed out to the console:

```
$ ./usr/bin/wine ~/NovaLogic/F-16\ Multirole\ Fighter\ -\ Single_Multiplayer\ Demo/f16demo.exe
wine: created the configuration directory '/home/<username>/.wine'
0012:err:ole:marshal_object couldn't get IPSFactory buffer for interface {00000131-0000-0000-c000-000000000046}
0012:err:ole:marshal_object couldn't get IPSFactory buffer for interface {6d5140c1-7436-11ce-8034-00aa006009fa}
0012:err:ole:StdMarshalImpl_MarshalInterface Failed to create ifstub, hres=0x80004002
0012:err:ole:CoMarshalInterface Failed to marshal the interface {6d5140c1-7436-11ce-8034-00aa006009fa}, 80004002
0012:err:ole:get_local_server_stream Failed: 80004002
0014:err:ole:marshal_object couldn't get IPSFactory buffer for interface {00000131-0000-0000-c000-000000000046}
0014:err:ole:marshal_object couldn't get IPSFactory buffer for interface {6d5140c1-7436-11ce-8034-00aa006009fa}
0014:err:ole:StdMarshalImpl_MarshalInterface Failed to create ifstub, hres=0x80004002
0014:err:ole:CoMarshalInterface Failed to marshal the interface {6d5140c1-7436-11ce-8034-00aa006009fa}, 80004002
0014:err:ole:get_local_server_stream Failed: 80004002
Could not load wine-gecko. HTML rendering will be disabled.
0026:err:module:load_so_dll failed to load .so lib "/home/<username>/wine/usr/bin/../lib32/wine/l3codeca.acm.so": libmpg123.so.0: cannot open shared object file: No such file or directory
0026:err:winediag:gnutls_initialize failed to load libgnutls, no support for encryption
0026:err:winediag:gnutls_initialize failed to load libgnutls, no support for pfx import/export
0026:err:module:load_so_dll failed to load .so lib "/home/<username>/wine/usr/bin/../lib32/wine/mp3dmod.dll.so": libmpg123.so.0: cannot open shared object file: No such file or directory
0028:err:winediag:gnutls_initialize failed to load libgnutls, no support for encryption
Could not load wine-gecko. HTML rendering will be disabled.
0026:err:module:load_so_dll failed to load .so lib "/home/<username>/wine/usr/bin/../lib32/wine/winegstreamer.dll.so": libgstvideo-1.0.so.0: cannot open shared object file: No such file or directory
0009:err:process:__wine_kernel_init boot event wait timed out
wine: configuration in '/home/<username>/.wine' has been updated.
0009:err:module:load_so_dll failed to load .so lib "/home/<username>/wine/usr/bin/../lib32/wine/l3codeca.acm.so": libmpg123.so.0: cannot open shared object file: No such file or directory
002d:err:module:load_so_dll failed to load .so lib "/home/<username>/wine/usr/bin/../lib32/wine/l3codeca.acm.so": libmpg123.so.0: cannot open shared object file: No such file or directory
0031:err:module:load_so_dll failed to load .so lib "/home/<username>/wine/usr/bin/../lib32/wine/l3codeca.acm.so": libmpg123.so.0: cannot open shared object file: No such file or directory
```

The game will be installed into the `~/.wine/drive_c/f16/` directory (which can be manually specified in one of the installer GUI dialogs):

```
$ cd ~/.wine/drive_c/f16/
$
$ ls -al
total 45216
drwxr-xr-x 2 <username> <usergroup>     4096 Jul 24 20:10 .
drwxr-xr-x 8 <username> <usergroup>     4096 Jul 24 20:10 ..
-rw-r--r-- 1 <username> <usergroup>     5285 Sep 15  1998 Appstr.bin
-rw-r--r-- 1 <username> <usergroup>      264 Sep 28  1998 Browser.htm
-rw-r--r-- 1 <username> <usergroup>       50 Sep 14  1998 Censor.txt
-rw-r--r-- 1 <username> <usergroup>       28 Sep 17  1998 checkftp.bat
-rw-r--r-- 1 <username> <usergroup> 30861914 Sep 29  1998 Common.pff
-rw-r--r-- 1 <username> <usergroup>      234 Aug  5  1998 F16.cfg
-rwxr-xr-x 1 <username> <usergroup>  1627136 Sep 29  1998 f16demo.exe
-rw-r--r-- 1 <username> <usergroup>  1317600 Sep 23  1998 F16demo.sbf
-rw-r--r-- 1 <username> <usergroup>    17194 Sep 28  1998 F16.inp
-rw-r--r-- 1 <username> <usergroup>       16 Sep 28  1998 F16.key
-rw-r--r-- 1 <username> <usergroup> 10639469 Sep 29  1998 F16.pff
-rw-r--r-- 1 <username> <usergroup>      652 Sep 28  1998 F16.sav
-rw-r--r-- 1 <username> <usergroup>     4133 Aug 18  1998 F16.txt
-rw-r--r-- 1 <username> <usergroup>       84 Sep 29  1998 F16.wiz
-rw-r--r-- 1 <username> <usergroup>    97280 Sep 16  1998 Hw_3dfx.dll
-rw-r--r-- 1 <username> <usergroup>   921656 Aug 31  1998 Init.bmp
-rw-r--r-- 1 <username> <usergroup>   277776 Nov  3  1997 Msvcrt.dll
-rw-r--r-- 1 <username> <usergroup>    17920 Aug 24  1998 Netsock.dll
-rwxr-xr-x 1 <username> <usergroup>   102912 Sep  8  1998 Novawrld.exe
-rw-r--r-- 1 <username> <usergroup>    11897 Apr 15  1998 Nwlogo.pcx
-rwxr-xr-x 1 <username> <usergroup>    74240 Sep 23  1998 Pack.exe
-rwxr-xr-x 1 <username> <usergroup>    31744 Feb 19  1998 Respack.exe
-rwxr-xr-x 1 <username> <usergroup>    29696 Apr  2  1998 Revupdat.exe
-rw-r--r-- 1 <username> <usergroup>      264 Sep 28  1998 Startup.htm
-rw-r--r-- 1 <username> <usergroup>      961 Apr 15  1998 Texture.pcx
-rw-r--r-- 1 <username> <usergroup>     4447 Jul 24 20:10 Uninst.isu
-rw-r--r-- 1 <username> <usergroup>       20 Sep 14  1998 Updated.pff
-rwxr-xr-x 1 <username> <usergroup>   160256 Sep 11  1998 Update.exe
-rw-r--r-- 1 <username> <usergroup>       84 Sep 29  1998 Update.wiz
```

Since the main game executable `f16demo.exe` is in fact a Windows PE32 executable...

```
$ file f16demo.exe
f16demo.exe: PE32 executable (GUI) Intel 80386, for MS Windows
```

...it needs to be launched using Wine:

```
$ ~/wine/usr/bin/wine f16demo.exe
0009:err:module:load_so_dll failed to load .so lib "/home/<username>/wine/usr/bin/../lib32/wine/l3codeca.acm.so": libmpg123.so.0: cannot open shared object file: No such file or directory
```

Playing Well &ndash; Flying Smart ! :+1:
