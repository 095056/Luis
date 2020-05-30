# Termux Developer's Wiki

General information about using Termux build environment, porting packages and
maintaining APT repository.

User's Wiki is available at https://wiki.termux.com/wiki/Main_Page.

## Git repositories

All source code that belongs to Termux is split between repositories available under
our organisation on [Github](https://github.com): https://github.com/termux.

We maintain a mirror of our projects on [Gitlab](https://gitlab.com/termux-mirror).

*Support of Android OS versions 5.x - 6.x is discontinued as of 01.01.2020!*

### Application and add-ons

All apks are being distributed through [Google Play](https://play.google.com/store/apps/developer?id=Fredrik+Fornwall), [F-Droid](https://search.f-droid.org/?q=Termux) and [Kali Nethunter Store](https://store.nethunter.com/en/packages/#q=Termux).

Builds on F-Droid and Kali Nethunter Store are done on their own and signed with different certificates.
Thus, application and add-ons obtained from different source can't be mixed.

* [termux-app](https://github.com/termux/termux-app): terminal emulator application sources.
* [termux-api](https://github.com/termux/termux-api): Termux:API add-on sources.
* [termux-boot](https://github.com/termux/termux-boot): Termux:Boot add-on sources.
* [termux-failsafe](https://github.com/termux/termux-failsafe):
* [termux-float](https://github.com/termux/termux-float): Termux:Float add-on sources.
* [termux-styling](https://github.com/termux/termux-styling): Termux:Styling add-on sources.
* [termux-tasker](https://github.com/termux/termux-tasker): Termux:Tasker add-on sources.
* [termux-x11](https://github.com/termux/termux-x11): Termux:X11 add-on sources. Unmaintained.

### Packages

Package definitions, build scripts and patches are split between multiple repositories
depending on their functionality.

* [termux-packages](https://github.com/termux/termux-packages): main set of packages and build environment.
* [game-packages](https://github.com/termux/game-packages): set of games.
* [science-packages](https://github.com/termux/science-packages): set of scientific packages.
* [termux-root-packages](https://github.com/termux/termux-root-packages): set of packages requiring device to be rooted.
* [unstable-packages](https://github.com/termux/unstable-packages): untested and potentially unstable packages.
* [x11-packages](https://github.com/termux/x11-packages): set of packages for X Window System.

### Package-specific repositories

We maintain some projects which are used for special purposes.

Packages:
* [TermuxAm](https://github.com/termux/TermuxAm): an activity manager for Android OS.
* [command-not-found](https://github.com/termux/command-not-found): utility to suggest packages if executed command not found.
* [libandroid-shmem](https://github.com/termux/libandroid-shmem): System V shared memory implementation through Android's ashmem.
* [libandroid-support](https://github.com/termux/libandroid-support): implementation of functionality missing in Bionic libc.
* [play-audio](https://github.com/termux/play-audio): utility to play audio files through OpenSLES.
* [proot](https://github.com/termux/proot): an Android-compatible fork of [proot](https://proot-me.github.io/).
* [termux-api-package](https://github.com/termux/termux-api-package): command line interface to Termux:API.
* [termux-apt-repo](https://github.com/termux/termux-apt-repo): script for generating APT repository from given packages.
* [termux-auth](https://github.com/termux/termux-auth): an implementation of password authentication for use with OpenSSH and similar packages.
* [termux-create-package](https://github.com/termux/termux-create-package): utility to create DEB package from set of files and metadata definition.
* [termux-elf-cleaner](https://github.com/termux/termux-elf-cleaner): utility to remove unused sections from ELF binaries.
* [termux-exec](https://github.com/termux/termux-exec): `LD_PRELOAD` hook for fixing `/bin` and `/sbin` path accesses during execution of `execve()` system call.
* [termux-services](https://github.com/termux/termux-services): scripts for managing services in Termux.

Other:
* [termux.github.io](https://github.com/termux/termux.github.io): Termux home page website.
* [termux-packaging](https://github.com/termux/termux-packaging): utilities to work with packages and generate bootstrap archives.

### External Resources Links

- [Android changes for NDK developers](https://android.googlesource.com/platform/bionic/+/master/android-changes-for-ndk-developers.md)
- [Linux From Scratch](http://www.linuxfromscratch.org/lfs/view/stable/)
- [Beyond Linux From Scratch](http://www.linuxfromscratch.org/blfs/view/stable/)
- [OpenWrt](https://openwrt.org/) as an embedded Linx distribution contains [patches and build scripts](https://dev.openwrt.org/browser/packages)
- [Kivy recipes](https://github.com/kivy/python-for-android/tree/master/pythonforandroid/recipes) contains recipes for building packages for Android.
