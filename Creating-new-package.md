## General requirements

- No operations requiring root privileges.

- No operations modifying files outside of build directory or `$TERMUX_PREFIX`.

- All scripts must be formatted according [Coding guideline](./Coding-guideline).

## Writing a package script

Package script (`build.sh`) is a Bash script that contains definitions for
metadata and (if needed) instructions for Termux build system how to build the
package. Such script is internally [used](./Building-packages#understanding-build-process)
by `./build-package.sh` and is not standalone.

Example of minimal working package build script:
```
# http(s) link to package home page.
TERMUX_PKG_HOMEPAGE=https://www.gnu.org/software/ed/

# One-line, short package description.
TERMUX_PKG_DESCRIPTION="Classic UNIX line editor"

# License.
TERMUX_PKG_LICENSE="GPL-2.0"

# Who cares about package.
# Specify yourself (Github nick, or name + email) if you wish to maintain the
# package, fix its bugs, etc. Otherwise specify "@termux".
# Please note that unofficial repositories are not allowed to reference @termux
# as their maintainer.
TERMUX_PKG_MAINTAINER="@termux"

# Version.
TERMUX_PKG_VERSION=1.15

# URL to archive with source code.
TERMUX_PKG_SRCURL=https://mirrors.kernel.org/gnu/ed/ed-${TERMUX_PKG_VERSION}.tar.lz

# SHA-256 checksum of the source code archive.
TERMUX_PKG_SHA256=ad4489c0ad7a108c514262da28e6c2a426946fb408a3977ef1ed34308bdfd174
```
Note that order of fields like shown above is preferred. In example above also
no build step overrides as expected that internal ones are enough to successfully
build the package.

`./build-package.sh` can automatically detect following build systems:

- Autotools

- CMake

- Meson

If you need to pass some additional arguments, use the field
`TERMUX_PKG_EXTRA_CONFIGURE_ARGS`.

### Table of available package control fields

| Order | Variable | Required | Description |
| -----:|:-------- |:--------:|:----------- |
| 1     | `TERMUX_PKG_HOMEPAGE` | yes | Home page URL. |
| 2     | `TERMUX_PKG_DESCRIPTION` | yes | Short, one-line description of package. |
| 3     | `TERMUX_PKG_LICENSE` | yes | Package license. |
| 4     | `TERMUX_PKG_MAINTAINER` | no | Package maintainer. |
| 5     | `TERMUX_PKG_API_LEVEL` | no | Android API level for which package should be compiled. |
| 6     | `TERMUX_PKG_VERSION` | yes | Original package version. |
| 7     | `TERMUX_PKG_REVISION` | no | Package revision. Bumped on each package rebuild. |
| 8     | `TERMUX_PKG_SKIP_SRC_EXTRACT` | no | Whether to omit source code downloading and extraction. Default is **false**. |
| 9     | `TERMUX_PKG_SRCURL` | not, if source extraction was skipped | URL from which source archive should be downloaded. |
| 10    | `TERMUX_PKG_SHA256` | not, if source URL was not set | SHA-256 checksum of source archive. |
| 11    | `TERMUX_PKG_GIT_BRANCH` | no | Branch to checkout in termux_step_git_clone_src. Default is `v$TERMUX_PKG_VERSION`. |
| 11    | `TERMUX_PKG_METAPACKAGE` | no | Whether to make package treated as metapackage. Default is **false**. |
| 12    | `TERMUX_PKG_DEPENDS` | no | Comma-separated list of dependency package names. |
| 13    | `TERMUX_PKG_BUILD_DEPENDS` | no | Comma-separated list of build-time only dependencies. |
| 14    | `TERMUX_PKG_BREAKS` | no | Comma-separated list of packages that are incompatible with the current one. |
| 15    | `TERMUX_PKG_CONFLICTS` | no | Comma-separated list of packages which have file name collisions with the current one. |
| 16    | `TERMUX_PKG_REPLACES` | no | Comma-separated list of packages being replaced by current one. |
| 17    | `TERMUX_PKG_PROVIDES` | no | Comma-separated list of virtual packages being provided by current one. |
| 18    | `TERMUX_PKG_RECOMMENDS` | no | Comma-separated list of non-absolute dependencies - packages usually used with the current one. |
| 19    | `TERMUX_PKG_SUGGESTS` | no | Comma-separated list of packages that are related to or enhance the current one. |
| 20    | `TERMUX_PKG_ESSENTIAL` | no | Whether to treat package as essential which cannot be uninstalled in usual way. Default is **false**. |
| 21    | `TERMUX_PKG_NO_STATICSPLIT` | no | Whether to split static libraries into a subpackage. Default is **false**. |
| 22    | `TERMUX_PKG_BUILD_IN_SRC` | no | Whether to perform build in a source code directory. Default is **false**. |
| 23    | `TERMUX_PKG_HAS_DEBUG` | no | Whether debug builds are possible for package. Default is **true**. |
| 24    | `TERMUX_PKG_PLATFORM_INDEPENDENT` | no | Whether to treat package as platform independent. Default is **false**. |
| 25    | `TERMUX_PKG_BLACKLISTED_ARCHES` | no | Comma-separated list of CPU architectures for which package cannot be compiled. |
| 26    | `TERMUX_PKG_HOSTBUILD` | no | Whether package require building for host. Default is **false**. |
| 27    | `TERMUX_PKG_FORCE_CMAKE` | no | Whether to force use CMake even if Autotools configure script available. Default is **false**. |
| 28    | `TERMUX_PKG_EXTRA_CONFIGURE_ARGS` | no | Extra arguments passed to build system configuration utility. |
| 29    | `TERMUX_PKG_EXTRA_HOSTBUILD_CONFIGURE_ARGS` | no | Extra arguments passed to build system configuration utility when performing host build. |
| 30    | `TERMUX_PKG_EXTRA_MAKE_ARGS` | no | Extra arguments passed to utility `make`. |
| 31    | `TERMUX_PKG_MAKE_INSTALL_TARGET` | no | Equivalent for `install` argument passed to utility `make` in the installation process. |
| 32    | `TERMUX_PKG_RM_AFTER_INSTALL` | no | List of files that should be removed after installation process. |
| 33    | `TERMUX_PKG_CONFFILES` | no | A space or newline separated list of package configuration files that should not be overwritten on update. |

### Table of available build step overrides

Complete reference for all build steps can be found in
[Building packages](./Building-packages#build-steps-reference).

| Execution order | Function name | Description |
| ---------------:|:-------------:|:----------- |
| 1               | `termux_step_get_source` | Obtain package source code and put it in `$TERMUX_PKG_SRCDIR`. |
| 2               | `termux_step_post_get_source` | Hook to run commands immediately after obtaining source code. |
| 3               | `termux_step_handle_host_build` | Determine whether a host build is required. |
| 4               | `termux_step_host_build` | Perform a host build. |
| 5               | `termux_step_pre_configure` | Hook to run commands before source configuration. |
| 6               | `termux_step_configure` | Configure sources. By default, it determines build system automatically. |
| 7               | `termux_step_post_configure` | Hook to run commands immediately after configuration. |
| 8               | `termux_step_make` | Compile the source code. |
| 9               | `termux_step_make_install` | Install the compiled artifacts. |
| 10              | `termux_step_post_make_install` | Hook to run commands immediately after installation. |
| 11              | `termux_step_install_license` | Link or copy package-specific LICENSE to `./share/doc/$TERMUX_PKG_NAME`. |
| 12              | `termux_step_post_massage` | Final hook before creating `*.deb` file(s). |
| 13              | `termux_step_create_debscripts` | In this step you can create ./preinst, ./postinst, ./prerm or ./postrm scripts which will be executed during the package installation or removing. |

## Writing a subpackage script

Subpackage definitions are often used to move optional parts of installation to
a separate packages. For example, some libraries come with utilities which may
not be used by end user. Thus we can move these utilities to a separate package
and reduce installation size in case when library package was installed as
dependency.

Minimal subpackage script consist of the following fields:
```
TERMUX_SUBPKG_DESCRIPTION= # Sub-package description
TERMUX_SUBPKG_INCLUDE="" # List of files (either space or newline separated) to include in subpackage
```
Order above is preferred as include list may be long.

Subpackage script must be located in same directory as `build.sh` and have file
name in the following format:
```
{subpackage name}.subpackage.sh
```
Note that its name cannot be same as of parent package.

Additional notes about subpackages:

- Subpackages always have version equal to parent package.

- Subpackages for static libraries are created automatically.

### Table of available subpackage control fields

| Order | Variable | Required | Description |
| -----:|:-------- |:--------:|:----------- |
| 1     | `TERMUX_SUBPKG_DESCRIPTION` | yes | Short, one-line description of subpackage. |
| 2     | `TERMUX_SUBPKG_DEPEND_ON_PARENT` | no | Specifies way how subpackage should depend on parent. See [Subpackage dependencies](#subpackage-dependencies) for more information. |
| 3     | `TERMUX_SUBPKG_DEPENDS` | no | Comma-separated list of subpackage dependencies. |
| 4     | `TERMUX_SUBPKG_BREAKS` | no | Comma-separated list of packages that are incompatible with the current one. |
| 5     | `TERMUX_SUBPKG_CONFLICTS` | no | Comma-separated list of packages which have file name collisions with the current one. |
| 6     | `TERMUX_SUBPKG_REPLACES` | no | Comma-separated list of packages being replaced by current one. |
| 7     | `TERMUX_SUBPKG_ESSENTIAL` | no | Whether to treat subpackage as essential which cannot be uninstalled in usual way. Default is **false**. |
| 8     | `TERMUX_SUBPKG_PLATFORM_INDEPENDENT` | no | Whether to treat subpackage as platform independent. Default is **false**. |
| 9     | `TERMUX_SUBPKG_INCLUDE` | yes | A space or newline separated list of files to be included in subpackage. |
| 10    | `TERMUX_SUBPKG_CONFFILES` | no | A space or newline separated list of package configuration files that should not be overwritten on update. |

#### Subpackage dependencies

By default subpackage depends only on parent package with current version. This
behaviour can be changed by setting variable `TERMUX_SUBPKG_DEPEND_ON_PARENT`.

Allowed values are:

- `deps` - subpackage will depend on dependencies of parent package.

- `unversioned` - subpackage will depend on parent package without specified
  version.

## Reserved variables in package scripts

Among with variables listed above (i.e. control fields), certain variables have
special purpose and used internally by `./build-package.sh`. They should not
be modified in runtime unless there is a good reason.

- `TERMUX_ON_DEVICE_BUILD` - If set, assume that building on device.

- `TERMUX_BUILD_IGNORE_LOCK` - If set to `true`, ignore build process lock.

- `TERMUX_BUILD_LOCK_FILE` - Path to build process lock file.

- `TERMUX_HOST_PLATFORM` - Host platform definition. Usually `$TERMUX_ARCH-linux-android`.

- `TERMUX_PKG_BUILDDIR` - Path to build directory of current package.

- `TERMUX_PKG_BUILDER_DIR` - Path to directory where located `build.sh` of
  current package.

- `TERMUX_PKG_BUILDER_SCRIPT` - Path to `build.sh` of current package.

- `TERMUX_PKG_CACHEDIR` - Path to source cache directory of current package.

- `TERMUX_PKG_MASSAGEDIR` - Path to directory where package content will be
  extracted from `$TERMUX_PREFIX`.

- `TERMUX_PKG_PACKAGEDIR` - Path to directory where components of `*.deb` archive
  of current package will be created.

- `TERMUX_PKG_SRCDIR` - Path to source directory of current package.

- `TERMUX_PKG_TMPDIR` - Path to temporary directory specific for current package.

- `TERMUX_COMMON_CACHEDIR` - Path to global cache directory where build tools
  are stored.

- `TERMUX_SCRIPTDIR` - Path to directory with utility scripts.

- `TERMUX_PKG_NAME` - Name of current package.

- `TERMUX_REPO_URL` - Array of APT repository URLs from which dependencies will
  be downloaded if `./build-package.sh` got option `-i` or `-I`.

- `TERMUX_REPO_DISTRIBUTION` - Array of distribution names in addition for
  `TERMUX_REPO_URL`.

- `TERMUX_REPO_COMPONENT` - Array of repository component names in addition for
  `TERMUX_REPO_URL`.
