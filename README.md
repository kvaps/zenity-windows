# Zenity for Windows

## Description

Zenity is a utility used to add GUI forms to scripts and receive feedback from the user. It was designed for use with Linux and GNOME. It uses GTK+ and GLADE libraries. The official website for Zenity is: http://live.gnome.org/Zenity. I have ported the latest version (3.20.0) of this software to Windows (win32).

## Screenshot

![](http://www.placella.com/software/zenity/zenity-win32.png)

## Downloads

 * Win32 installer
   * [zenity-3.20.0_win32-1.exe](https://github.com/kvaps/one-connect/releases/download/v3.20.0-1/zenity-3.20.0_win32-1.exe)
   * [MD5.SUM](https://github.com/kvaps/zenity-windows/blob/master/MD5.SUM)
 * Source code
   * http://ftp.gnome.org/pub/gnome/sources/zenity/

## How to build from source:

__Warning: this is my personal experience, correct as of October 2009 for Zenity 3.20.0, your results may vary!__

1. Install cygwin, and coose following packages:

```
curl
patch
recode
gcc-g++
pkg-config
itstool
make
gettext-devel
```
   *I also install `recode`, it's not obligatory, you may to not do this.*

2. Download GTK+ Bundle for Windows (http://www.tarnyko.net/dl/gtk.htm) extract it to `C:\gtk`

3. Execute commands:  

```
curl -O http://ftp.gnome.org/pub/gnome/sources/zenity/3.20/zenity-3.20.0.tar.xz
tar xvf zenity-3.20.0.tar.xz
cd zenity-3.20.0
curl -O https://github.com/kvaps/zenity-windows/blob/master/zenity-3.20.0_win32-1.patch
patch < zenity-3.20.0_win32-1.patch

export GTK_BASEPATH=/cygdrive/c/gtk
export LIB=$GTK_BASEPATH/lib
export PKG_CONFIG_PATH=$GTK_BASEPATH/lib/pkgconfig
mkdir /opt
mount -o bind /cygdrive/c/gtk/ /opt

./configure --prefix=
make
make install DESTDIR=/opt

cp /bin/cygwin1.dll /opt/bin/
cp /bin/cygintl-8.dll /opt/bin/
cp /bin/cygiconv-2.dll /opt/bin/
cp /bin/recode.exe /opt/bin/
cp /bin/cygrecode-0.dll /opt/bin/

umount /opt
```

4. Rename `C:\gtk` to `C:\zenity` and create installer package from it.

## Special thanks

* http://www.placella.com/software/zenity/
* http://hxcaine.com/blog/2013/05/21/compile-gtk-code-with-cygwin-tutorial/
* http://help.ubuntu.ru/wiki/programs_installation

