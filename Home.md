## Termux Developer's Wiki

General information about using Termux build environment, porting packages and
maintaining APT repository.

User's Wiki available at https://wiki.termux.com/wiki/Main_Page.

### Git branches

1. Branch "master":

   Main source tree with packages built for Android API 24. Therefore this branch
   also referred as `android-7`.

   Corresponds to APT repository `https://dl.bintray.com/termux/termux-packages-24/`.

2. Branch "android-5":

   Legacy source tree with packages built for Android API 21 and used for
   supporting devices with old Android versions.

   Corresponds to APT repository `https://termux.net`.

### External Resources Links

- [Android changes for NDK developers](https://android.googlesource.com/platform/bionic/+/master/android-changes-for-ndk-developers.md)

- [Linux From Scratch](http://www.linuxfromscratch.org/lfs/view/stable/)

- [Beyond Linux From Scratch](http://www.linuxfromscratch.org/blfs/view/stable/)

- [OpenWrt](https://openwrt.org/) as an embedded Linx distribution contains [patches and build scripts](https://dev.openwrt.org/browser/packages)

- [Kivy recipes](https://github.com/kivy/python-for-android/tree/master/pythonforandroid/recipes) contains recipes for building packages for Android.
