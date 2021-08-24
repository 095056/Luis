[![asciicast](https://asciinema.org/a/5BsCbNoCzNFEgcH8vh8975MLm.svg)](https://asciinema.org/a/5BsCbNoCzNFEgcH8vh8975MLm?autoplay=1&speed=2.5)

## How to build package

Once you have properly [configured](https://github.com/termux/termux-packages/wiki/Build-environment)
the build environment, you may start to build packages. Build is started by
executing script `build-package.sh` located at the root of termux-packages
repository with passing package name as argument.

Example of building package `bash` for architecture `arm`:
```
./build-package.sh -a arm bash
```

Of you need to build several packages, specify them all on command line.
Example:
```
./build-package.sh bash coreutils htop
```

### Build options

Script `build-package.sh` accepts several options that affect build behaviour.

- `-a` - The architecture to build for. Accepted values are: aarch64, arm, i686,
  x86_64. Default is `aarch64`. For on-device builds architecture is determined
  automatically and this option is not available.

- `-d` - Build with debug information and turn of compiler optimizations.

- `-D` - Build disabled package, i.e. located in directory `./disabled-packages`.

- `-f` - Force build package even if it already built or installed.

- `-i` - Download dependencies instead of building them. Erases data in
  `TERMUX_PREFIX` before starting build. Not available for on-device builds.

- `-I` - Download dependencies instead of building them. Unlike option above,
  this one does not erase data in `$TERMUX_PREFIX` and available for on-device
  builds.

- `-q` - Pass necessary arguments to `make` or similar tool to make build quiet.
  May not work for all packages.

- `-c` - Continue previous build, skip source extraction and configure step and go straight to termux_step_make. Only works if you first run a normal build, and it fails or you stop it during termux_step_make or later.

- `-s` - Skip dependency check.

- `-o` - Specify directory where to place built \*.deb files. Default is
  `./debs`.

## Understanding build process

Build starts at the moment of execution of `./build-package.sh` script and is
split into the following stages (environment initialization steps are omitted):

1. Source the `./packages/$TERMUX_PACKAGE_NAME/build.sh` to obtain metadata such
   like version, description, dependencies, source URL and package-specific
   build steps.

2. In case if `build-package.sh` got arguments `-i` or `-I`, download \*.deb
   files from APT repository and extract to `$TERMUX_PREFIX`.

   Otherwise obtain the dependency build order from script `./scripts/buildorder.py`
   and execute `./build-package.sh` with argument `-s` for each dependency package.

3. Create timestamp file which will be used later.

4. Download package's source code from the URL and verify its SHA-256 checksum.
   Then extract source code to `$TERMUX_PKG_SRCDIR`. This step is omitted if
   `$TERMUX_PKG_SKIP_SRC_EXTRACT` is set.

5. Build package for the host. This step is performed only when
   `TERMUX_PKG_HOSTBUILD` is set.

6. Set up a standalone Android NDK toolchain and apply NDK sysroot patches.
   This step is performed only one time.

7. Search for patches in `./packages/$TERMUX_PKG_NAME/*.patch` and apply them.

8. Configure and compile source code for specified `$TERMUX_ARCH`.

9. Install everything into `$TERMUX_PREFIX`.

10. Determine files which are modified from time when timestamp file was created
    (step 3) and extract them into `$TERMUX_TOPDIR/$TERMUX_PKG_NAME/massage`.

11. Strip binaries (if non-debug build), gzip manpages, delete unwanted files
    and fix permissions. Distribute files between subpackages if needed.

12. Archive package data into \*.deb files ready for distribution.

## Build steps reference

Order specifies function sequence. 0 order specifies utility functions.

Suborder specifies a function triggered by the main function. Functions with
different suborders are not executed simultaneously.

| Order | Function Name | Overridable | Description |
| -----:|:-------------:| -----------:|:----------- |
| 0.1   | `termux_error_exit` | no | Stop script and output error. |
| 0.2   | `termux_download` | no | Utility function to download any file. |
| 0.3   | `termux_setup_golang` | no | Setup Go Build environment. |
| 0.4   | `termux_setup_cmake` | no | Setup CMake configure system. |
| 0.5   | `termux_setup_ninja` | no | Setup Ninja make system. |
| 0.6   | `termux_setup_meson` | no | Setup Meson configure system. |
| 0.7   | `termux_setup_protobuf` | no | Setup Protobuf compiler. |
| 0.8   | `termux_setup_rust` | no | Setup Cargo Build. |
| 1     | `termux_step_setup_variables` | no | Setup essential variables like directory locations and flags. |
| 2     | `termux_step_handle_buildarch` | no | Determine architecture to build for. |
| 3     | `termux_step_setup_build_folders` | no | Delete old src and build directories if they exist. |
| 4     | `termux_step_start_build` | no | Initialize build environment. Source package's `build.sh`. |
| 5     | `termux_step_get_dependencies` | no | Download or build specified dependencies of the package. |
| 5.1   | `termux_step_get_repo_files` | no | Fetch APT packages information when `-i` or `-I` option was supplied. |
| 5.2   | `termux_extract_dep_info` | no | Obtain package architecture and version for downloading. |
| 6     | `termux_step_create_timestamp_file` | no | Make timestamp to determine which files have been installed by the build. |
| 5.3   | `termux_download_deb` | no | Download dependency `*.deb` packages for installation. |
| 6     | `termux_step_get_source` | yes | Obtain package source code and put it in `$TERMUX_PKG_SRCDIR`. |
| 7.1   | `termux_git_clone_src` | no | Obtain source by git clone, is run if `$TERMUX_PKG_SRCURL` ends with ".git". |
| 7.2   | `termux_download_src_archive` | no | Download zip or tar archive with package source code. |
| 7.3   | `termux_unpack_src_archive` | no | Extract downloaded archive into `$TERMUX_PKG_SRCDIR`. |
| 8     | `termux_step_post_get_source` | yes | Hook to run commands immediately after obtaining source code. |
| 9     | `termux_step_handle_host_build` | yes | Determine whether a host build is required. |
| 9.1   | `termux_step_host_build` | yes | Perform a host build. |
| 10     | `termux_step_setup_toolchain` | no | Setup NDK standalone toolchain. |
| 11    | `termux_step_patch_package` | no | Apply to source code all `*.patch` files located in package's directory. |
| 12    | `termux_step_replace_guess_scripts` | no | Replace `config.sub` and `config.guess` scripts. |
| 13    | `termux_step_pre_configure` | yes | Hook to run commands before source configuration. |
| 14    | `termux_step_configure` | yes | Configure sources. By default, it determines build system automatically. |
| 14.1  | `termux_step_configure_autotools` | no | Autotools build configuration. |
| 14.2  | `termux_step_configure_cmake` | no | CMake build configuration. |
| 14.3  | `termux_step_configure_meson` | no | Meson build configuration. |
| 15    | `termux_step_post_configure` | yes | Hook to run commands immediately after configuration. |
| 16    | `termux_step_make` | yes | Compile the source code. |
| 17    | `termux_step_make_install` | yes | Install the compiled artifacts. |
| 18    | `termux_step_post_make_install` | yes | Hook to run commands immediately after installation. |
| 19    | `termux_step_install_service_scripts` | yes | Installs scripts for termux-services |
| 20    | `termux_step_install_license` | yes | Link or copy package-specific LICENSE to `./share/doc/$TERMUX_PKG_NAME`. |
| 21    | `termux_step_extract_into_massagedir` | no with `make_install` | Extract files modified in `$TERMUX_PREFIX`. |
| 22    | `termux_step_massage` | no | Strip binaries, remove unneeded files. |
| 22.1  | `termux_create_subpackages` | no | Creates all subpackages. |
| 24    | `termux_step_post_massage` | yes | Final hook before creating `*.deb` file(s). |
| 25    | `termux_step_create_datatar` | no | Archive package files. |
| 26    | `termux_step_create_debfile` | no | Create `*.deb` package. |
| 26.1  | `termux_step_create_debscripts` | yes | Create maintainer scripts, e.g. pre/post installation hooks. |
| 27    | `termux_step_finish_build` | no | Notification of finish. |

## Tips and tricks
 
### Building from a local git repository

If you want to build a package from a local repository you can set
`TERMUX_PKG_SRCURL=file:///path/to/local/repo.git`. The folder name
has to end with .git, so if you for example want to build
termux-api-package run:

```sh
git clone https://github.com/termux/termux-api-package termux-api-package.git
cd termux-api-package.git
# make changes, commit them and maybe create a tag
cd /path/to/termux-packages
# edit packages/termux-api-build.sh, set:
#   `TERMUX_PKG_SRCURL=file:///path/to/termux-api-package.git`
# you also need to update TERMUX_PKG_VERSION to match the tag you set.
# If you want to build from master (or another branch) rather than a tag you can set
#   `TERMUX_PKG_GIT_BRANCH="master"`
./build-package.sh termux-api-package
```
