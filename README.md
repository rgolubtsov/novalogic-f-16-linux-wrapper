# NovaLogic F-16 Multirole Fighter Playable Demo Linux Wrapper :small_blue_diamond: :airplane:

Copy the game distribution's self-extracting InstallShield installation executable from a CD to the hard drive:

```
$ sudo mount /dev/cdrom ./mnt
mount: /home/<username>/mnt: WARNING: device write-protected, mounted read-only.
$
$ mount
...
/dev/sr0 on /home/<username>/mnt type iso9660 (ro,relatime,norock,check=r,map=n,blocksize=2048)
$
$ cp -vR ./mnt/novalogic .
'./mnt/novalogic' -> './novalogic'
'./mnt/novalogic/f16demo' -> './novalogic/f16demo'
'./mnt/novalogic/f16demo/f16demo.exe' -> './novalogic/f16demo/f16demo.exe'
$
$ sudo umount ./mnt
$
$ eject
```

Download the `wine` package along with all its necessary dependencies as Pacman proposes to do that, but do not install any of them including **Wine** itself (supposing the host OS is Arch Linux):

```
$ sudo pacman -Syw wine
:: Synchronizing package databases...
...
resolving dependencies...

Packages (6) lib32-gettext-0.22.5-1  lib32-libnl-3.11.0-1  lib32-libpcap-1.10.5-2  lib32-libxkbcommon-1.8.0-1  lib32-libxrandr-1.5.4-1
             wine-10.1-1

Total Download Size:  218.34 MiB

:: Proceed with download? [Y/n]
...
$
$ ls -al /var/cache/pacman/pkg/wine-10.1-1-x86_64.pkg.tar.zst
-rw-r--r-- 1 root root 227293025 Feb  8 12:33 /var/cache/pacman/pkg/wine-10.1-1-x86_64.pkg.tar.zst
```

Create a directory where to extract the `wine` package and do extract it there:

```
$ mkdir wine && cd wine && tar -xf /var/cache/pacman/pkg/wine-10.1-1-x86_64.pkg.tar.zst
$
$ ls -al
total 252
drwxr-xr-x  3 <username> <usergroup>   4096 Feb 15 18:20 .
drwx------ 11 <username> <usergroup>  12288 Feb 15 18:20 ..
-rw-r--r--  1 <username> <usergroup>  14401 Feb  8 12:25 .BUILDINFO
-rw-r--r--  1 <username> <usergroup>    202 Feb  8 12:25 .INSTALL
-rw-r--r--  1 <username> <usergroup> 212048 Feb  8 12:25 .MTREE
-rw-r--r--  1 <username> <usergroup>   3529 Feb  8 12:25 .PKGINFO
drwxr-xr-x  7 <username> <usergroup>   4096 Feb  8 12:25 usr
```

It is possible trying to run the game distribution's self-extracting InstallShield installation executable as is and check it out using the `file` command to make sure it is in fact a Windows PE32 executable:

```
$ ls -al ../novalogic/f16demo/f16demo.exe
-rwxr-xr-x 1 <username> <usergroup> 25469793 Dec  3  2019 ../novalogic/f16demo/f16demo.exe
$
$ ../novalogic/f16demo/f16demo.exe
bash: ../novalogic/f16demo/f16demo.exe: cannot execute binary file: Exec format error
$
$ file ../novalogic/f16demo/f16demo.exe
../novalogic/f16demo/f16demo.exe: PE32 executable (GUI) Intel 80386, for MS Windows, InstallShield self-extracting archive, 5 sections
```

From now on the use of **Wine** is required to launch the installation. During launching of **Wine** it may probably ask to install *Wine Mono* and *Wine Gecko* support libraries &ndash; discard them anyway and ignore any errors like the following ones, printed out to the console:

```
$ ./usr/bin/wine ../novalogic/f16demo/f16demo.exe
003c:err:service:process_send_start_message service L"PlugPlay" failed to start
003c:fixme:service:scmdatabase_autostart_services Auto-start service L"PlugPlay" failed to start: 1053
0188:fixme:msg:pack_message msg 14 (WM_ERASEBKGND) not supported yet
0188:err:winediag:gnutls_process_attach failed to load libgnutls, no support for encryption
0188:err:winediag:process_attach failed to load libgnutls, no support for pfx import/export
002c:err:setupapi:do_file_copyW Unsupported style(s) 0x10
002c:err:setupapi:do_file_copyW Unsupported style(s) 0x10
0068:err:setupapi:do_file_copyW Unsupported style(s) 0x10
002c:err:setupapi:do_file_copyW Unsupported style(s) 0x10
0068:err:setupapi:do_file_copyW Unsupported style(s) 0x10
01d0:fixme:ntdll:NtQuerySystemInformation info_class SYSTEM_PERFORMANCE_INFORMATION
01d0:err:sync:RtlpWaitForCriticalSection section 781439E0 "../wine/dlls/krnl386.exe16/syslevel.c: Win16Mutex" wait timed out in thread 01d0, blocked by 01d4, retrying (60 sec)
01dc:err:seh:dispatch_user_callback ignoring exception c0000005
01dc:err:seh:dispatch_user_callback ignoring exception c0000005
01dc:err:seh:dispatch_user_callback ignoring exception c0000005
```

The game will be installed into the `~/.wine/drive_c/f16/` directory (which can be manually specified in one of the installer GUI dialogs):

```
$ cd ~/.wine/drive_c/f16/
$
$ ls -al
total 45232
drwxr-xr-x 2 <username> <usergroup>     4096 Feb 15 19:07 .
drwxr-xr-x 8 <username> <usergroup>     4096 Jul 26  2019 ..
-rw-r--r-- 1 <username> <usergroup>      193 Jul 26  2019 APP.INI
-rw-r--r-- 1 <username> <usergroup>     5285 Sep 15  1998 Appstr.bin
-rw-r--r-- 1 <username> <usergroup>      264 Sep 28  1998 Browser.htm
-rw-r--r-- 1 <username> <usergroup>       50 Sep 14  1998 Censor.txt
-rw-r--r-- 1 <username> <usergroup>       28 Sep 17  1998 checkftp.bat
-rw-r--r-- 1 <username> <usergroup> 30861914 Sep 29  1998 Common.pff
-rw-r--r-- 1 <username> <usergroup>      234 Aug  5  1998 F16.cfg
-rwxr-xr-x 1 <username> <usergroup>  1627136 Sep 29  1998 f16demo.exe
-rw-r--r-- 1 <username> <usergroup>  1317600 Sep 23  1998 F16demo.sbf
-rw-r--r-- 1 <username> <usergroup>       17 Aug 20  2019 F16.inf
-rw-r--r-- 1 <username> <usergroup>    17194 Sep 28  1998 F16.inp
-rw-r--r-- 1 <username> <usergroup>       16 Sep 28  1998 F16.key
-rw-r--r-- 1 <username> <usergroup> 10639469 Sep 29  1998 F16.pff
-rw-r--r-- 1 <username> <usergroup>      652 Sep 28  1998 F16.sav
-rw-r--r-- 1 <username> <usergroup>     4133 Aug 18  1998 F16.txt
-rw-r--r-- 1 <username> <usergroup>       84 Sep 29  1998 F16.wiz
-rw-r--r-- 1 <username> <usergroup>    97280 Sep 16  1998 Hw_3dfx.dll
-rw-r--r-- 1 <username> <usergroup>   921656 Aug 31  1998 Init.bmp
-rw-r--r-- 1 <username> <usergroup>     3508 Sep  8  2019 _inptmap.txt
-rw-r--r-- 1 <username> <usergroup>   277776 Nov  3  1997 Msvcrt.dll
-rw-r--r-- 1 <username> <usergroup>    17920 Aug 24  1998 Netsock.dll
-rw-r--r-- 1 <username> <usergroup>      584 Aug 20  2019 novaftp.log
-rwxr-xr-x 1 <username> <usergroup>   102912 Sep  8  1998 Novawrld.exe
-rw-r--r-- 1 <username> <usergroup>    11897 Apr 15  1998 Nwlogo.pcx
-rwxr-xr-x 1 <username> <usergroup>    74240 Sep 23  1998 Pack.exe
-rwxr-xr-x 1 <username> <usergroup>    31744 Feb 19  1998 Respack.exe
-rwxr-xr-x 1 <username> <usergroup>    29696 Apr  2  1998 Revupdat.exe
-rw-r--r-- 1 <username> <usergroup>      264 Sep 28  1998 Startup.htm
-rw-r--r-- 1 <username> <usergroup>      961 Apr 15  1998 Texture.pcx
-rw-r--r-- 1 <username> <usergroup>     5320 Feb 15 19:07 Uninst.isu
-rw-r--r-- 1 <username> <usergroup>       20 Sep 14  1998 Updated.pff
-rwxr-xr-x 1 <username> <usergroup>   160256 Sep 11  1998 Update.exe
-rw-r--r-- 1 <username> <usergroup>       84 Sep 29  1998 Update.wiz
```

Since the main game executable `f16demo.exe` is in fact a Windows PE32 executable...

```
$ file f16demo.exe
f16demo.exe: PE32 executable (GUI) Intel 80386, for MS Windows, 6 sections
```

...it needs to be launched using **Wine**:

```
$ ~/wine/usr/bin/wine f16demo.exe
001c:err:plugplay:load_function_driver AddDevice failed for driver L"winebus", status 0xc0000002.
0016:err:ntoskrnl:ZwLoadDriver failed to create driver L"\\Registry\\Machine\\System\\CurrentControlSet\\Services\\nsiproxy": c0000142
000f:fixme:service:scmdatabase_autostart_services Auto-start service L"nsiproxy" failed to start: 1114
0016:err:ntoskrnl:ZwLoadDriver failed to create driver L"\\Registry\\Machine\\System\\CurrentControlSet\\Services\\NDIS": 00000001
000f:fixme:service:scmdatabase_autostart_services Auto-start service L"NDIS" failed to start: 731
```

Playing Well &ndash; Flying Smart ! :+1:
