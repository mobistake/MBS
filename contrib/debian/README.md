
Debian
====================
This directory contains files used to package mbsd/mbs-qt
for Debian-based Linux systems. If you compile mbsd/mbs-qt yourself, there are some useful files here.

## pivx: URI support ##


mbs-qt.desktop  (Gnome / Open Desktop)
To install:

	sudo desktop-file-install mbs-qt.desktop
	sudo update-desktop-database

If you build yourself, you will either need to modify the paths in
the .desktop file or copy or symlink your mbs-qt binary to `/usr/bin`
and the `../../share/pixmaps/mbs128.png` to `/usr/share/pixmaps`

mbs-qt.protocol (KDE)

