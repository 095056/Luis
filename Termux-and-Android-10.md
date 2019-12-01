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

### Launching shell under proot

Proot is used to execute binaries from paths where SELinux applies noexec restriction. This approach may be considered as Google Play policy violation, however it allows to keep current environment with only small changes and all packages functioning.

Working PoC: https://github.com/xeffyr/termux-app/releases/tag/v0.84-prooted2

*Note*: proot allows to make Termux FHS-compatible with dropping all path-fixing patches and make Termux usable as secondary user.

### Embedding packages into APK file

That solution does not met Termux requirements because Android does not allow to store arbitrary files in JNI lib directory.

## Issues

* Android 10 does not allow free access to `/sdcard` (at least file system based).
