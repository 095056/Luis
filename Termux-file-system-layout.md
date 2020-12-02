Android OS normally does not provide a write access to system directories such as root file system ("/")
for the reasons of security and integrity of system files. This makes difficulties to follow the
[Filesystem Hierarchy Standard](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard) and Termux
has to use own.

## Packages installation root

All packages must install their data into this directory (installation prefix):
```
/data/data/com.termux/files/usr
```
For safety of user data, it is not allowed to create packages installing files outside of this directory.

We often refer to this path as `$PREFIX` or `$TERMUX_PREFIX`, latter is used within the context of packaging.

#### Termux file system hierarchy table

| Path                          | Purpose          |
|:------------------------------|:-----------------|
|`${TERMUX_PREFIX}/bin`         | Executables used by shell. Combines `/bin`, `/sbin`, `/usr/bin`, `/usr/sbin`.|
|`${TERMUX_PREFIX}/etc`         | Configuration files.|
|`${TERMUX_PREFIX}/include`     | C/C++ headers.|
|`${TERMUX_PREFIX}/lib`         | Shared objects (libraries), runtime executable data or development-related.|
|`${TERMUX_PREFIX}/libexec`     | Executables which should not be run by user directly.|
|`${TERMUX_PREFIX}/opt`         | Installation root for sideloaded packages.|
|`${TERMUX_PREFIX}/share`       | Non-executable runtime data and documentation.|
|`${TERMUX_PREFIX}/tmp`         | Temporary files. Erased on each application restart. Combines `/tmp` and `/var/tmp`. *Can be freely modified by user.*|
|`${TERMUX_PREFIX}/var`         | Variable data, such as caches and databases. *Can be modified by user, but with additional care.*|
|`${TERMUX_PREFIX}/var/run`     | Lock files, PID files, sockets and other temporary files created by daemons. Replaces `/run`.|

> Important: do not be confused by prefix directory `.../usr`. It has nothing to do with the real `/usr`
directory which you can find in Linux distributions. Termux never uses a secondary file system hierarchy
(`/usr`) for the packaging purposes.

All hardcoded references to FHS directories should be patched.

## Home directory

Termux home directory lives outside of the package installation prefix and is located at this path:
```
/data/data/com.termux/files/home
```

This is a place where all user data should be stored. As all application internal data is typically stored
on EXT4 or F2FS file system, it supports file access modes, executable permission and special files like
symbolic links.

Packages should never install files to the home directory. Exception is only for .deb file scripts, they
can be used to prepare initial configuration in $HOME for packages which can't do it on their own.

## Android directories

Android OS provides a number of directories, some of them are FHS-compliant. All system directories are
read-only and packages should never attempt to install or delete something in them.

| Path | Description                                       |
|------|---------------------------------------------------|
|`/`   | The root file system. Usually it is a ramdisk, but on modern Android OS versions it is a mounted system partition. Can be restricted by SELinux and not be viewable by `ls`.|
|`/bin`| Symbolic link to `/system/bin`. Do not add this to PATH to prevent clash of Termux tools with ones provided by Android.|
|`/dev`| Standard mount point for file system with device files. Access can be restricted by SELinux, though all important world-writable devices are accessible.|
|`/etc`| Symbolic link to `/system/etc`.|
|`/mnt`| Raw mount points of file systems with application and user data.|
|`/proc`| Standard directory with runtime process and kernel information. Typically mounted with `hidepid=2` option for privacy.|
|`/proc/net`| Networking interface statistics. Access restricted since Android 10 for privacy reasons.|
|`/sbin`| Directory where special-purpose executables (ADB daemon, dm-verity helper, modem nvram loader, etc). Access is restricted by SELinux and file modes. Do not add this directory to PATH.|
|`/storage`| Mounted user's storage volumes. Like `/mnt` but drive file systems are provisioned by `sdcardfs` daemon.|
|`/system`| The Android OS installation root.|
|`/system/bin`| A basic set of command line tools for system purposes and fully-functional ADB shell. Avoid adding this to PATH. Exceptions are allowed only for alternate executable paths, e.g. in case if package is not installed.|
|`/system/xbin`| Optional set of system command line tools. Content may vary between ROMs. Do not add this to PATH.|