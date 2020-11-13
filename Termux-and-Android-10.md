Due to SDK behavior changes and new Google Play policy, Termux does not receive
updates on Play Store anymore. Install the application and add-ons from F-Droid
instead.

# A brief explanation about Android 10 problem

Google requires the target SDK level to be set to at least 29, which corresponds
to Android OS version 10. But due to new operating system behavior changes we
cannot do so and have to use SDK level 28.

https://developer.android.com/about/versions/10/behavior-changes-all#execute-permission:
> Untrusted apps that target Android 10 cannot invoke exec() on files within
the app's home directory. This execution of files from the writable app home
directory is a W^X violation. Apps should load only the binary code that's
embedded within an app's APK file.

Related issue: https://github.com/termux/termux-app/issues/1072

*We do not want to introduce the breaking changes to comply with Google's
requirements. But as result Termux does not support Android 10 officially.*

Please note that users of Android 10 may face these restrictions:
* On certain devices Termux will not start shell. Workaround is to set
  SELinux to permissive mode - only possible on rooted devices.

* Access to `/proc/net` is restricted. As result `netstat` and other
  utilities using data from this interface does not work anymore.
  On rooted devices run these utilities as superuser to get them
  working again.

People using Android 11 may experience more issues, for example some
utilities are being terminated by file descriptor sanitizer.
