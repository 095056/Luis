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

## Why distribute packages in APKs ?

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

## Additional Android 10 issues

* Android 10 does not allow free access to `/sdcard` (at least file system based) due
  to scoped storage.
