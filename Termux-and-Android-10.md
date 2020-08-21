# Summary
Termux does not target API 29 (Android 10) due to
https://developer.android.com/about/versions/10/behavior-changes-all#execute-permission:

> Untrusted apps that target Android 10 cannot invoke exec() on files within
the app's home directory. This execution of files from the writable app home
directory is a W^X violation. Apps should load only the binary code that's
embedded within an app's APK file.

Until November 2, 2020, Termux has to change its package management solution
to met requirements of the new Android SELinux policy and Google Play rules.
Otherwise Termux will no longer be able to receive application updates.

Issue with discussion: https://github.com/termux/termux-app/issues/1072.

*Accodring to tests by @xeffyr, this issue may not affect users running Lineage
OS 17.x ROMs.*

## How this issue is going to be solved?

As Android OS of version 10 and higher requires executable code to be
distributed within the APK file, we will convert our .DEB files into APK
format by placing files into JNI lib directory. Termux application will
automatically detect these APKs and will map JNI files into $PREFIX through
symbolic links.

Termux will also provide a tiny package manager which will help to deal with
APKs.

This solution will completely met all requirements of the new Android OS. Also,
it helps to separate a user-space from package installation and will make
environment much more easier for recovery as package data will be read-only.

Apt package manager will be removed because it no longer will be usable.

Development is done in https://github.com/termux/termux-app/tree/android-10.

### Converting .DEB to .APK demo

[![asciicast](https://asciinema.org/a/A3Ge2dwz7m6Y4RTayTSOwX2qN.svg)](https://asciinema.org/a/A3Ge2dwz7m6Y4RTayTSOwX2qN?speed=2.0)

Sample packages can be obtained from http://staging.termux-mirror.ml/android-10/.

### Alternate solutions

We know that APK-based package distribution will make Termux non-convenient or
unusable for some users.

We had a discussion on Android 10 solutions and there were enough time to
provide a working one. We got suggestions from using `proot` as binary loader
to extremelly ridiculous variants like "rewrite packages in WASM".

As none decided to make a pull request with implementation of their ideas and
also most of them will make package maintaining impossible for us, we are
picking an APK-based packaging variant.

## Additional notes about Termux and SDK-29

* Users updating Termux compiled with SDK-28 to application compiled with SDK-29,
  will not face the `execve()` restriction.

* On some devices, `execve()` is restricted even for SDK <=28, so any Termux build
  doesn't work on them.

* Termux compiled with SDK-29 will lose access to shared storage `/sdcard` due to
  forced scoped storage. Termux:API command `termux-storage-get` can be used for
  retrieving files. However, to save files a private directory should be used.

* Lineage OS 17 ROM (Android 10 based) does not restrict `execve()` for SDK-29
  but free access to storage is lost anyway. Tested with engineering (eng) userdebug
  build.

* Access to /proc/net is restricted for all applications. Utilities like `netstat` are
  not working anymore. (Lineage OS 17 does not restrict)

* Termux:API: `termux-wifi-enable` is no-op on SDK-29. (only when both Termux
  and Termux:API are compiled with target SDK 29)

* Termux:API: `termux-telephony-deviceinfo` will not show IMEI on SDK-29.

## Android 11+ issues

* [Package visibility](https://developer.android.com/preview/privacy/package-visibility)
  restricts access to the list of installed applications. Perhaps Termux app should add the
  https://developer.android.com/reference/kotlin/android/Manifest.permission#query_all_packages.
