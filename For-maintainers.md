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

- `./scripts/list-packages.sh`:
  List all packages with a one-line summary.

- `scripts/package_uploader.sh`:
  Upload packages to Bintray.

## CI/CD

We use [Cirrus CI](https://cirrus-ci.com/) for:

- Building Docker image when `./scripts/Dockerfile` was modified.

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

- `%ci:no-build` - tell CI to immediately finish build with "green" status.

- `%ci:reset-backlog` - tell CI to build changes only from latest pushed commit.

### Dealing with CI issues

1. Build job failed but several new commits were pushed and now build always
   fails due to timeout.

   Reason: changes are determined between last commit that which passed CI build
   (green status) and the latest pushed one. Be careful before submitting new
   changes !

   Solution: either submit empty commit with tag `%ci:no-build` or with useful
   payload and tag `%ci:reset-backlog`. If branch was "master", make sure that
   all necessary packages are built and uploaded.

2. Build is done successfully, but upload is not because log shows
   `tar: Unexpected EOF in archive`.

   Reason: upload is done in a separate task and to make \*.deb files be available
   for upload, they are archived and passed through http cache which may not be
   always available.

   Solution: re-run upload task. Re-run all tasks in case of failure. If does not
   help, better then build & upload packages manually.

3. Build is done successfully, but upload is not because log shows
   `This resource requires authentication`.

   Reason: invalid credentials were supplied to upload script.

   Solution: make sure that supplied credentials are correct & up-to-date and
   try again. Also check https://www.githubstatus.com/ - if Github has some
   issues, then credentials may not be decrypted on CI.

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

TODO: fill this
