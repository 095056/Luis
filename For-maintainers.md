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

- `./scripts/package_uploader.sh`:
  Upload packages to Bintray.

## CI/CD

We use [Cirrus CI](https://cirrus-ci.com/) for:

- Building Docker image when `./scripts/Dockerfile` was modified.

- Performing basic error checks for all `build.sh` scripts.

- Building updated packages when related `build.sh` were modified.

- Building packages modified in pull requests.

- Upload modified packages to [Bintray](https://bintray.com/termux) (only branch 'master').

Configuration file [`./.cirrus.yml`](https://github.com/termux/termux-packages/blob/master/.cirrus.yml)
and dispatcher script [`./scripts/build/ci/cirrus-ci_dispatcher.sh`](https://github.com/termux/termux-packages/blob/master/scripts/build/ci/cirrus-ci_dispatcher.sh)
are managed by [@xeffyr](https://github.com/xeffyr).

All builds are publically visible and available at https://cirrus-ci.com/github/termux/termux-packages.

### Available commit tags

Tags are special text strings placed on dedicated line in git commit text. While
it is possible to insert any text inside git commit, the *tags* are allowed for
use only by maintainers.

- `%ci:no-build` - tell CI to immediately finish build with "green" status. Has no
  effect on linter task.

- `%ci:reset-backlog` - tell CI to build changes only from latest pushed commit. Has
  no effect on linter task.

### Dealing with CI issues

1. Build job failed but several new commits were pushed and now build always
   fails due to timeout.

   Reason: changes are determined between last commit that which passed CI build
   (green status) and the latest pushed one. Be careful before submitting new
   changes !

   Solution: either submit empty commit with tag `%ci:no-build` or with useful
   payload and tag `%ci:reset-backlog`. If branch was "master", make sure that
   all necessary packages are built and uploaded.

2. Upload failed, log shows `This resource requires authentication`.

   Reason: invalid credentials were supplied to upload script.

   Solution: make sure that supplied credentials are correct & up-to-date and
   try again. Also check https://www.githubstatus.com/ - if Github has some
   issues, then credentials may not be decrypted on CI.

3. Upload failed, log shows `skipping because no files to upload`.

   Reason: certain packages didn't have revision bumped and were downloaded
   as dependency for other package (we use `build-package.sh` with `-I` option
   set). Thus uploader script cannot find related `*.deb` files.

   Solution: just ignore as packages with non-modified version will not be
   re-submitted to APT repository anyway. But next submitted commit probably
   will require tag `%ci:reset-backlog`.

4. Upload failed, log shows `Error occurred while uploading`.

   Reason: network connection failure or remote server cannot handle request.

   Solution: re-submit package with bumped revision as metadata on remote can
   be inconsistent.

## Uploading packages (Bintray)

Upload is done by executing script `./scripts/package_uploader.sh` with package
name as argument. Note that \*.deb files must have name in format `{name}_{full-version}_{arch}.deb`.
It is expected that \*.deb files are located in `./debs`, but can be changed by
passing argument `-p /path/to/deb_dir`.

Example:
```
./scripts/package_uploader.sh -p ./my_built_packages bash
```

Authentication credentials are supplied through environment variables:

`BINTRAY_USERNAME`        - User name on [Bintray](https://bintray.com).

`BINTRAY_API_KEY`         - Personal API key on [Bintray](https://bintray.com).

`BINTRAY_GPG_PASSPHRASE`  - A passphrase for your GPG key stored on [Bintray](https://bintray.com).

Any operations (except download) on APT repository can be done only by
maintainers who have *write* access.

### Deleting packages

To delete package from APT repository, use pass argument `-d` with list of
package names to `package_uploader.sh`:
```
./scripts/package_uploader.sh -d {package names}
```

**Warning:** never delete packages when upload is not finished. This may result
in metadata inconsistency.

### Deleting old versions

*We keep old versions only for technical reasons - to prevent 404 errors when
users download packages.*

Pass argument `-c` with list of packages which should be cleaned. Example:
```
./scripts/package_uploader.sh -c bash busybox coreutils libllvm
```

**Warning:** never clean versions when \*.deb files for specific architectures
were not updated. This will made package unavailable for some devices.

### Regenerating metadata

In certain cases you may need to force-regenerate metadata. This can be done in
following way:
```
./scripts/package_uploader.sh -r
```

## Generating bootstrap archives

Bootstrap archives is a zip archives of `$TERMUX_PREFIX` with basic packages
preinstalled and used to create a minimal working environment on first start
of Termux application.

Utilities to generate bootstrap archives available in https://github.com/termux/termux-packaging
repository. Highly recommended to use script located in [scripts/generate-bootstraps.sh](https://github.com/termux/termux-packaging/blob/master/scripts/generate-bootstraps.sh).

Termux bootstraps (that used for `https://dl.bintray.com/termux/termux-packages-24`)
are generated with the following command:
```
./generate-bootstraps.sh
```

Default script configuration is
```
Architectures: aarch64 arm i686 x86_64
Repository URL: https://dl.bintray.com/termux/termux-packages-24
Prefix: /data/data/com.termux/files/usr
```
so if you want to generate bootstraps for custom repository, consider using
following command line options:

- `--architectures` - Comma separated list of architectures for which bootstraps
  should be generated.

- `--prefix` - `$TERMUX_PREFIX` against which your packages are built.

- `--repository` - URL of your APT repository. Offline bootstrap generation is not
  supported.
