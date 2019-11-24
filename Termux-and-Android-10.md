## Summary
Termux does not target API 29 (Android 10) due to
https://developer.android.com/about/versions/10/behavior-changes-all#execute-permission:

> Untrusted apps that target Android 10 cannot invoke exec() on files within
the app's home directory. This execution of files from the writable app home
directory is a W^X violation. Apps should load only the binary code that's
embedded within an app's APK file.

In the long run this needs to be fixed and Termux needs to update its target API.
This page is for gathering ideas and information about how to work around this.

Issue with discussion: https://github.com/termux/termux-app/issues/1072.

## Solution

We are going to embed package data inside APKs (placing binaries in native library
directory) as this is only the most reliable solution.

It has few issues that should be resolved:

* How package data should be stored in APK ? Should we store everything inside
  native library directory or only binaries should be here ? How to deal with
  symlinks ?

* How to deal with packages having native extensions (ruby, python) ? Can be fixed
  if everything is in native library directory, but what if it is not ?

To fix problem with user's executables, we may use `proot` either session-widely
or only for specific files.

Other (app-specific) issues:

* Android 10 does not allow free access to `/sdcard` (at least file system based).
