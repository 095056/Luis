## Structure

Files and directories available inside build environment:

- `./debs` - directory where built packages will be placed. Does not exist by
  default.

- `./disabled-packages` - directory with packages excluded from main build tree
  due to various reasons.

- `./ndk-patches` - directory with patches for Android NDK sysroot.

- `./packages` - directory where all packages (scripts and patches) are
  located.

- `./sample` - sample structure for creating new package.

- `./scripts` - internal parts of build system and some utility scripts.

- `./build-all.sh` - script for building all available packages.

- `./build-package.sh` - script for building one or more packages.

- `./clean.sh` - script for cleaning build environment.

## Setting up

### Docker container

Using official Docker image is a recommended way for building Termux packages
which ensures that you have same environment as Termux maintainers and therefore
builds are reproducible.

If you have Docker installed and running, then launching build environment
should be as simple as running
```
./scripts/run-docker.sh
```
Wait until latest image will be downloaded and then container's shell prompt
should appear. The `termux-packages` folder will be mounted as `/home/builder/termux-packages`.

You may execute commands inside container without launching interactive shell
by supplying them as arguments to `./scripts/run-docker.sh`. Example:
```
./scripts/run-docker.sh ./build-package.sh libandroid-support
```

Sometimes Docker image should be updated. Following command will update image
and delete outdated container:
```
./scripts/update-docker.sh
```

#### Building own Docker image

`Dockerfile` is [located](https://github.com/termux/termux-packages/blob/master/scripts/Dockerfile)
in `./scripts/` directory and configured to build Ubuntu-based image.

To build the Docker image, execute following commands:
```
cd ./scripts
docker build -t termux/package-builder .
```

If you are getting error like `-bash: /tmp/setup-ubuntu.sh: Permission denied`,
make sure that all `*.sh` files have permission `755` and `umask` is 0022.

#### Docker on Windows

For Windows users there is a PowerShell script available:
```
.\scripts\run-docker.ps1
```

#### Tips

1. Multiple containers.

   You can have multiple containers running in parallel. Just set different
   container name as environment variable:
   ```
   CONTAINER_NAME=termux_builder_2 ./scripts/run-docker.sh
   ```

2. Using unofficial Docker image.

   You can use a custom Docker image as environment variable `TERMUX_BUILDER_IMAGE_NAME`,
   but it also recommended to set a custom name for the container (like above):
   ```
   export TERMUX_BUILDER_IMAGE_NAME=username/termux-custom-builder
   export CONTAINER_NAME=custom-builder1
   ./scripts/run-docker.sh
   ```

### VirtualBox VM

There is a [Vagrantfile](https://github.com/termux/termux-packages/blob/master/scripts/Vagrantfile)
for setting up a VirtualBox Ubuntu installation.

- Run `vagrant plugin install vagrant-disksize` to install disksize plugin for
  Vagrant.

- Run `cd scripts && vagrant up` to setup and launch the virtual machine.

- Run `vagrant ssh` to ssh into the virtual machine.

### Host OS

We have scripts that automate installation of packages used in build process.
For now only Ubuntu and Arch Linux distributions are supported. Note that all
scripts execute commands under `sudo`.

For Ubuntu:
```
./scripts/setup-ubuntu.sh
```

For Arch Linux:
```
./scripts/setup-archlinux.sh
```

Additionally you will need to install Android SDK and NDK. By default, it
is expected that both SDK and NDK are installed into `$HOME/lib`, so it is
recommended to use following script to properly setup them:
```
./scripts/setup-android-sdk.sh
```

## Termux

Our build system can be used to build packages on device. Though with some
limitations as our build scripts expect that utilities used at run time available
outside of Termux prefix (sysroot).

**Warning:** devices on which `termux-exec` is not working are unsupported !

If you wish to use your Termux installation, execute the following command inside
the root directory of cloned `termux-package` repository:
```
./scripts/setup-termux.sh
```

Note that files generated in build process are installed to `$PREFIX` and are
not tracked by package manager. It also highly recommended to backup both `$HOME`
and `$PREFIX` before building any package.

## Changing default behaviour

Following environment variables affect behaviour of Termux build system:

- `TERMUX_TOPDIR` - Specifies the base directory for Termux build environment.
  Standalone toolchain, downloaded sources, package build directories will be
  created here. Default is `$HOME/.termux-build`.

- `TERMUX_MAKE_PROCESSES` - Specifies amount of jobs that should be spawned by
  utility `make`. Default is output of command `nproc`.

- `TERMUX_PKG_API_LEVEL` - Specifies Android API level against which packages
  will be compiled. Default is 24 for branch "master" and 21 for branch "android-5".

- `TERMUX_PKG_MAINTAINER` - Specifies a value that should be written to package's
  maintainer field. Default is `Fredrik Fornwall @fornwall`.

- `TERMUX_PACKAGES_DIRECTORIES` - Specifies a root directory of package tree.
  Default is `packages`.

These variables are overridden with [arguments](./Building-packages#build-options)
of `./build-package.sh`:

- `TERMUX_ARCH` - Specifies CPU architecture for which packages should be
  cross-compiled. Default is `aarch64`. Cannot be changed when building on device.

- `TERMUX_DEBUG` - Perform debug build. Debug information won't be stripped from
  binaries and compiler optimizations will be turned off.

- `TERMUX_INSTALL_DEPS` - If set to `true`, then dependencies will be installed
  from the APT repository rather than built.

- `TERMUX_NO_CLEAN` - Special option for use with `TERMUX_INSTALL_DEPS`. If set
  to `true`, then Termux system root will not be wiped before extracting
  dependencies. When building on device, this variable should be always `true`.

- `TERMUX_QUIET_BUILD` - If set, additional arguments will be passed to utility
  `make` to reduce output in compilation process.

- `TERMUX_SKIP_DEPCHECK` - If set, then no dependency checks will be done.

- `TERMUX_DEBDIR` - Path to directory where built `*.deb` files will be placed.

Custom default values for environment variables can be set through file
`./scripts/properties.sh`.

## Important note about Termux prefix

In Termux, prefix is equivalent of the root file system on Linux distributions.

If you decided to change `$TERMUX_PREFIX`, you are on your own. It is not
possible to mix packages from different prefixes as changing one assumes that
compiled packages will never be used in a Termux environment.

Those who decided to change `$TERMUX_PREFIX` should change `$TERMUX_ANDROID_HOME`
as well to avoid path problems.
