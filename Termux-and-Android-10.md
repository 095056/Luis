## Summary
Termux does not target API 29 (Android 10) due to https://developer.android.com/about/versions/10/behavior-changes-all#execute-permission:

> Untrusted apps that target Android 10 cannot invoke exec() on files within the app's home directory. This execution of files from the writable app home directory is a W^X violation. Apps should load only the binary code that's embedded within an app's APK file.

In the long run this needs to be fixed and Termux needs to update its target API. This page is for gathering ideas and information about how to work around this.

Issue with discussion: https://github.com/termux/termux-app/issues/1072. Possible approaches to explore follows.

## 1. Distribute packages bundled in apps
With this approach packages would be inside normal Android apps distributed as normal. To lessen the amount of packages some grouping, where an app contains several related packages, would probably be needed.

## 2. Use proot to execute files
See https://github.com/termux/proot/commit/ebcfe01744a4a288df38f76c24a60ae8ab978240 for a proof of concept.

## 3. Generate an app on-device containing packages
When a user downloads a package it is merged into a package containing all user-installed packages (with the package being generated on-device). This app cannot be signed with the same key as the main app, is it possible to share without that?

