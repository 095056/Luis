## Utilities

- `./build-all.sh`:
  Build all packages in the correct order (using `./scripts/buildorder.py`).

- `./clean.sh`:
  Cleaning build environment.

- `./scripts/check-built-packages.py`:
  Compare local (git) and remote (apt) package versions.

- `./scripts/check-pie.sh`:
  Verify that all binaries are using PIE, which is required for Android 5+.

- `./scripts/check-versions.sh`:
  Check for package updates.

- `./scripts/ldd`:
  Print list of required shared libraries for given binary.

- `./scripts/lint-packages.sh`:
  Do basic checks for problems in `build.sh` scripts.

- `./scripts/list-packages.sh`:
  List all packages with a one-line summary.

- `./scripts/generate-bootstraps.sh`:
  Generate bootstrap archive for Termux app from published apt repo.

- `./scripts/build-bootstraps.sh`:
  Build bootstrap archive for Termux app from local package sources.

## Bootstraps

The Termux bootstrap zips contain the minimal environment/rootfs with basic packages required to run the [`termux-app`](https://github.com/termux/termux-app) for Termux context.

- Bootstraps are generated weekly/manual with [`termux-packages/scripts/generate-bootstraps.sh`](https://github.com/termux/termux-packages/blob/master/scripts/generate-bootstraps.sh) by [`termux-packages/bootstrap_archives` wokflow](https://github.com/termux/termux-packages/blob/master/.github/workflows/bootstrap_archives.yml) and uploaded to [`termux-packages` releases](https://github.com/termux/termux-packages/releases). Check https://github.com/termux/termux-packages/wiki/For-maintainers#generating-bootstrap-archives
- During `termux-app` build, the [`app/build.gradle`](https://github.com/termux/termux-app/blob/master/app/build.gradle) downloads the bootstrap zips from `termux-packages` releases into `app/src/main/cpp/` and verifies the checksum.
- The zips are added into the app APK as native libraries at `lib/<arch>/libtermux-bootstrap.so` inside the APK by [`app/src/main/cpp/termux-bootstrap-zip.S`](https://github.com/termux/termux-app/blob/master/app/src/main/cpp/termux-bootstrap-zip.S). You can rename the `libtermux-bootstrap.so` file to `libtermux-bootstrap.zip` and open it with a zip file viewer and bootstrap will exist with the name `.rodata`. 
- When app is installed, android extracts the `libtermux-bootstrap.so` file for the device's architecture to `<apk_install_path>/lib/<arch>` due to [`packagingOptions.jniLibs.useLegacyPackaging=true`](https://developer.android.com/reference/tools/gradle-api/7.1/com/android/build/api/dsl/JniLibsPackagingOptions#uselegacypackaging) in `app/build.gradle` (previously [`extractNativeLibs=true`](https://developer.android.com/guide/topics/manifest/application-element#extractNativeLibs) in `app/src/main/AndroidManifest.xml`). The exact installation path will depend on device depending on [`PackageManagerService`](https://cs.android.com/android/platform/superproject/+/android-12.0.0_r4:frameworks/base/services/core/java/com/android/server/pm/PackageManagerService.java;l=18952) ([`f56f1c5c`](https://cs.android.com/android/_/android/platform/frameworks/base/+/f56f1c5c587ed5af452ed1b339218dabc12c9f93)) and can be checked with `pm path com.termux` with `adb` or `root` or `dirname "$TERMUX_APP__APK_FILE_PATH"` in `termux-app` `>= v0.119.0`. If APK build is architecture specific like [github builds](https://github.com/termux/termux-app#github), then `libtermux-bootstrap.so` of only a single architecture will be added to APK to save space.
- When termux app is run and if `$PREFIX` is missing or "empty", then [`TermuxInstaller.setupBootstrapIfNeeded()`](https://github.com/termux/termux-app/blob/master/app/src/main/java/com/termux/app/TermuxInstaller.java) will call `loadZipBytes()` to load the `libtermux-bootstrap.so` library for the device's architecture with a call to `System.loadLibrary()` and get the zip with a call to the native [`getZip()`](https://github.com/termux/termux-app/blob/master/app/src/main/cpp/termux-bootstrap.c) function and then extract the bootstrap zip to `$PREFIX`.
- The current size of each bootstrap zip of an architecture is `~25MB`. So if an APK is built for all architectures (universal), then bootstrap zips of all `4` architectures will use `100MB`. If APK is built for a single architecture, then the single bootstrap zip will use `25MB`. The app code and resources will consume additional space. Since android will extract `libtermux-bootstrap.so` of the device's architecture to APK installation path, that will consume `25MB` additional space on the device. Then due to bootstrap zip extraction to `$PREFIX`, additional uncompressed space of `~70-80MB` will be consumed as well depending on filesystem and its block size. So total disk usage for universal APKs is `100+25+80=205MB` and for single architecture APKs is `25+25+80=130MB`. The [github builds](https://github.com/termux/termux-app#github) provide both universal and architecture specific APKs, but [F-Droid builds](https://github.com/termux/termux-app#f-droid) only provide universal APKs, since F-Droid does not support [split APKs](https://github.com/termux/termux-app/pull/1904).

### Generate bootstrap archives

The [`generate-bootstraps.sh`](https://github.com/termux/termux-packages/blob/master/scripts/generate-bootstraps.sh) is a script to generate bootstrap archives for the `termux-app` from debs published in an apt repo. Run `generate-bootstrap.sh --help` for more info.

Built archives will be available in the current working directory.

Please note that you must have an `apt` repository deployed on the web server in order to be able to generate bootstrap archives, which has debs built for the `TERMUX_APP_PACKAGE` in [`scripts/properties.sh`](https://github.com/termux/termux-packages/blob/master/scripts/properties.sh). You cannot use custom `TERMUX_APP_PACKAGE` with Termux app official repos/mirrors, since they publish packages for `com.termux` package. If you do not want to publish custom repo, use [`build-bootstraps.sh`](#build-bootstrap-archives) instead.

Default script configuration is
```
TERMUX_APP_PACKAGE: com.termux
TERMUX_PACKAGE_MANAGER: apt
TERMUX_ARCHITECTURES: aarch64 arm i686 x86_64
REPO_BASE_URL: https://packages-cf.termux.dev/apt/termux-main
```
so if you want to generate bootstraps for custom repository, consider using
following command line options:

- `--architectures` - Comma separated list of architectures for which bootstraps
  should be generated.

- `--repository` - URL of your APT repository. Offline bootstrap generation is not
  supported.


### Build bootstrap archives

The [`build-bootstraps.sh`](https://github.com/termux/termux-packages/blob/master/scripts/build-bootstraps.sh) is a script to build bootstrap archives for the `termux-app` from local package sources instead of debs published in apt repo like done by `generate-bootstrap.sh`. It allows bootstrap archives to be easily built for (forked) termux apps without having to publish an apt repo first. Run `build-bootstrap.sh --help` for more info.

The package name/prefix that the bootstrap is built for is defined by `TERMUX_APP_PACKAGE` in [`scripts/properties.sh`](https://github.com/termux/termux-packages/blob/master/scripts/properties.sh). It defaults to `com.termux`. If package name is changed, make sure to run `./scripts/run-docker.sh ./clean.sh` or pass `-f` to force rebuild of packages.

### Examples

Build default bootstrap archives for all supported archs:
`./scripts/run-docker.sh ./scripts/build-bootstraps.sh &> build.log`

Build default bootstrap archive for aarch64 arch only:
`./scripts/run-docker.sh ./scripts/build-bootstraps.sh --architectures aarch64 &> build.log`

Build bootstrap archive with additionall openssh package for aarch64 arch only:
`./scripts/run-docker.sh ./scripts/build-bootstraps.sh --architectures aarch64 --add openssh &> build.log`


### Build Termux App

The [`termux-app/app/build.gradle`](https://github.com/termux/termux-app/blob/v0.118.0/app/build.gradle#L196) downloads the bootstrap archives published by [`
Generate bootstrap archives
`](https://github.com/termux/termux-packages/actions/workflows/bootstrap_archives.yml) to [`termux-packages` releases](https://github.com/termux/termux-packages/releases) and verifies the checksums when building the app.

If you want to build `termux-app` with the custom bootstrap build, run `Build` -> `Clean Project` in Android Studio, then replace/place the built bootstrap `zips` in `termux-app/app/src/main/cpp`. Add a `return` statement in first line of [`downloadBootstrap()`](https://github.com/termux/termux-app/blob/v0.118.0/app/build.gradle#L196) function in `termux-app/app/build.gradle` to prevent function from running so that the custom `bootstrap-*.zip` files don't get replaced with downloaded ones and then sync project with gradle files and build the apk.
