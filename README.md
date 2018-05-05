# FriCAS for Cygwin64

[FriCAS](http://fricas.sourceforge.net/)  is a general purpose computer algebra system with a strong focus on mathematical research and development of new algorithms.  (details see [Wikipedia](https://en.wikipedia.org/wiki/FriCAS)). This project is about providing a fully functional version for [Cygwin64](https://cygwin.com/) (portable) including [Cygwin/X](https://x.cygwin.com/).  
Windows 10+ users may want to use [WSL](https://docs.microsoft.com/en-us/windows/wsl/about) instead of cygwin, however, a portable FriCAS for Windows might be of interest anyway.

## Portable Cygwin Version
Most comfortable is the *portable Cygwin* version from [MachinaCore](https://github.com/MachinaCore/CygwinPortable). However, we recommend the prebuilt versions from [AppVeyor](https://ci.appveyor.com/project/MachinaCore/cygwinportable/build/artifacts)    instead of the older 1.2 releases.

## Binary Releases (fricas)
There are [binary releases](https://github.com/nilqed/fricas_cygwin/releases) for the current FriCAS version 1.3.3:

* fricas-1.3.3-x86_64-cygwin.tar.gz (install to /usr/local)
* ecl-16.1.3.tar.gz (required if you don't have ECL already)

and
* FriCAS_CygwinPortable_1.3.3.7z

**FriCAS_CygwinPortable** will run out of the box. See below how it goes.


## Portable mode howto

1. Download FriCAS_CygwinPortable64_x.y.z.7z 
2. Unpack anywhere  (7z required)
3. Start `CygwinPortable.exe`

#### 4. Use tray menu
![Click tray icon](img/tray0.png)

![Scripts or](img/tray1.png)

#### 5. X server
![Start X](img/tray2.png)

![X server](img/tray3.png)

![X applications menu](img/tray4.png)

#### 6. Cygwin terminal (mintty)
![System tools](img/tray5.png)


### 7. FriCAS (Hypedoc/Draw)
![FriCAS 1](img/fricas1.png)

![FriCAS 2](img/fricas2.png)

![FriCAS 3](img/fricas3.png)



## Do it yourself

Get the latest release of CygwinPortable from  [AppVeyor](https://ci.appveyor.com/project/MachinaCore/cygwinportable/build/artifacts), then setup the suggested
system cygwin/X (use 64bit). Or, one may even start from scratch:

`git clone https://github.com/MachinaCore/CygwinPortable.git`


#### Get devel tools
```
wget rawgit.com/transcode-open/apt-cyg/master/apt-cyg
install apt-cyg /bin

apt-cyg searchall gcc
apt-cyg install gcc-g++
...
```
or, better, use the menu/setup in the tray.


#### Get ECL (Lisp)

`git clone https://gitlab.com/embeddable-common-lisp/ecl.git`

Build it accordingly.

```
configure/make ECL 
apt-cyg install dos2unix
dos2unix /home/cygwin/ecl/src/bdwgc/install-sh
make install
$ ecl --version
ECL 16.1.3
```

#### Get and build FriCAS

```
wget https://sourceforge.net/projects/fricas/files/fricas/1.3.3/fricas-1.3.3-full.tar.bz2

Make FriCAS
===========
install all libs according to the INSTALL doc

kfp@NUC: ~/fricas-1.3.3
$ ./configure --with-lisp=ecl
$ make
```

##### Caveats and workarounds

Emacs interface will not work.

```
Usual Error:
;;;
;;; Compiling /home/kfp/fricas-1.3.3/contrib/emacs/gen-cpl.lisp.
;;; OPTIMIZE levels: Safety=0, Space=0, Speed=3, Debug=0
;;;
;;; End of Pass 1.      0 [main] AXIOMsys 5652 child_info_fork::abort: address space needed by 'eclcRhyxv.dll' (0x130000) is already occupied

;;; Internal error:
;;;   ** Could not spawn subprocess to run "gcc".
   >> System error:
   NIL is not of type STREAM.

==========
Workaround
==========
cd contrib/emacs/
edit Makefile
Change:
 - default: efricas fricas-cpl.el
 + default: #efricas fricas-cpl.el

do make again ...
 
cp command.list fricas-1.3.3/target/x86_64-x-cygwin/lib/
make install
```











