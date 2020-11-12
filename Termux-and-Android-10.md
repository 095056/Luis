**Android 10 transition has been cancelled and as result Termux will not receive
updates on Play Store anymore.** Google policy for Android applications require
to bump target SDK level to at least 29, but we cannot do that due to Termux
application design.

Use Termux application and add-ons from F-Droid.

# What problem with Android 10?
That are all operating system behavior changes. Specifically, this one:
https://developer.android.com/about/versions/10/behavior-changes-all#execute-permission

> Untrusted apps that target Android 10 cannot invoke exec() on files within
the app's home directory. This execution of files from the writable app home
directory is a W^X violation. Apps should load only the binary code that's
embedded within an app's APK file.

Check also the issue related to code execution restrictions:
https://github.com/termux/termux-app/issues/1072.

Note that issue may not affect users with custom Android like Lineage OS, or
those who have SELinux in permissive mode.

## What is a possible solution for this issue?
According to Google Play policy and Android application design, we will have
to bundle packages inside APK files and distribute as regular applications -
just like we do currently with Termux add-ons (API, Widget, Float, etc). This
is the only viable solution in long-term.

Here are brief overview of the packaging changes:
* All files from .deb file are extracted and renamed to have .so as extension.
  These "shared libraries" are part of the APK file just like normal native
  code.
* A file mapping will be created and packaged inside APK as well. It will be
  needed to create symlinks from .so file in native lib directory to matching
  file inside $PREFIX (Termux system root).
* No `apt` and `dpkg` will be available. All basic package management functionality
  is done by Termux application. A tiny script will be present to allow package
  management from shell.
* Updated `termux-exec` `execve()` wrapper - now uses `proot` to run user
  binaries and bypass restrictions from SELinux. *As proot is unstable, not all
  users will be able to run custom binaries.*

Of course, that will have serious impact on user experience. From that point
Termux will no longer be same as was before. Many things likely will stop
working.

Development is done in https://github.com/termux/termux-app/tree/android-10.

### Alternate solutions

Do not like solution proposed by Termux maintainers, want to help to solve
issues on the latest Android OS versions and make Termux better? - Submit
your pull requests and we will figure out whether it would be better than
APK-based packaging.

Theoretical suggestions, especially ones like "custom binary loaders" or
something extremelly ridiculous like "rewrite everything in WASM" are NOT
ACCEPTED!

Suggestions to use `proot` to execute everything are not accepted. Proot
is not stable and still against Google Play policy. It also not known how
such solution will be viable in long-term.

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
