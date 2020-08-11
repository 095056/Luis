# Summary
Termux does not target API 29 (Android 10) due to
https://developer.android.com/about/versions/10/behavior-changes-all#execute-permission:

> Untrusted apps that target Android 10 cannot invoke exec() on files within
the app's home directory. This execution of files from the writable app home
directory is a W^X violation. Apps should load only the binary code that's
embedded within an app's APK file.

In the long run this needs to be fixed and Termux needs to update its target API.
This page is for information about how to work around this.

Issue with discussion: https://github.com/termux/termux-app/issues/1072.

SDK 29 transition deadline is November 2, 2020. After that date, Google Play will
not accept app updates without SDK level bumped to 29.

## How issue is going to be solved ?

Package \*.deb files will be transformed into APK file, where the data will be
placed into JNI lib directory which is marked executable by Android OS. That
makes package data to be read-only and overcome the SELinux restrictions applied.

During installation of such package the contents in JNI lib directory are symlinked
to `$PREFIX` mimicking the normal environment like a pre- Android 10 one. Package
management is handled by Termux application with command line interface exposed
through utility `pkg`. Apt package manager is going to be removed.

### Converting .DEB to .APK demo

[![asciicast](https://asciinema.org/a/A3Ge2dwz7m6Y4RTayTSOwX2qN.svg)](https://asciinema.org/a/A3Ge2dwz7m6Y4RTayTSOwX2qN?t=122&speed=2.0)

Sample packages can be obtained from http://termux.net/apks/.

Related pull request: https://github.com/termux/termux-app/pull/1427

### Why distribute packages in APKs ?

We choose to distribute packages in APKs because only that solution is correct.
Android package format expects native code to be placed in directory for JNI
libraries and that comply with W^X policy.

Of course that will made Termux "non-convenient" for users, but actually Termux
can have some benefits from that packaging format change. Here is what will be
possible with in-APK package distribution:
* Full offline installation.
* Integrity of package files. Since files are enforced to be read-only by Android
  OS, you can expect that they are immutable and can't be changed accidentally by
  script or something else.
* Easy package downgrading without having to mess with the correct dependency versions.
* Easy environment repair. It is possible to implement it as one-click action.

## Alternate solutions

There is a number of other solutions that were suggested during [discussion](https://github.com/termux/termux-app/issues/1072).

Please understand that we are not looking on other solutions beyond in-APK
packaging anymore. We already have one (WIP currently) which will require
minimal effort for maintaining and provide minimal feature loss. If you
want to suggest your solution, provide the related pull requests and be
ready to maintain it in case it will be accepted.

| Name             | Compatibility with Google Play policy\* | Notes                             |
|:-----------------|:---------------------------------------:|:----------------------------------|
| Keep SDK 28      | Not as minimum target SDK level increases each year. | Will render Termux incompatible with new devices and kill project in future. |
| PRoot            | No. It implements custom executable loader. | May cause issues with certain programs. May not work properly on some devices. |
| QEMU system mode | **Full or partial** (code is executed in emulator). | Low performance and environment isolation make it unsuitable for using Termux as terminal emulator for Android. |
| ~~[User-mode Linux](https://en.wikipedia.org/wiki/User-mode_Linux)~~ | No. Code is executed on host, can be treated as custom executable loader. | Is not available for ARM and AArch64. Termux developers can't port it on these architectures. Termux will not be able to run root packages properly. |
| ~~[Userland exec](https://github.com/bediger4000/userlandexec)~~ | No. It implements custom executable loader. | For x86_64 and glibc only. Termux developers are not going to port it. |
| ~~WASM~~             | **Full or partial** (depening on implementation). | There no people in Termux developers who wish to or can maintain WASM package ports and runtime. |

\* *Google Play policy restricts sideloading of executable code. See https://support.google.com/googleplay/android-developer/answer/9887877.*<br>
\*\* *Crossed variants are out-of-scope as can't be handled by maintainers.*

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
