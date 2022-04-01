# Haskell package guidelines

## Packing policy

For Haskell packages we follow [ArchLinux's policy](https://wiki.archlinux.org/title/Haskell_package_guidelines)
to only provide dynamic libs and executables by default, except that there is no seperate ghc-pkg database for
static packages.

Since there is no seperate ghc-pkg database for static packages, installing and using static libs should work
out of the box, without any extra work from users side.

See also: https://wiki.archlinux.org/title/Haskell

## Building

Although Termux build system can automatically build Haskell packages, still following paramaters are available for overriding default.

### Variables

Following variables store flags to be passed to `termux-ghc-setup` (specify them if overriding build steps):

- `TERMUX_HASKELL_LLVM_BACKEND` stores flags to enable LLVM Backend for archs other than `i686`.
- `TERMUX_HASKELL_OPTIMISATION` stores flags for level of optimisation of package depending on whether `TERMUX_DEBUG_BUILD` is `true` or `false`.

### Tools

GHC Cross compiler bins are available as following:

| Original name | Available as(during build) |
| ------------- | -------------------------- |
| ghc           | `termux-ghc`               |
| ghc-pkg       | `termux-ghc-pkg`           |
| hsc2hs        | `termux-hsc2hs`            |
| hp2ps         | `termux-hp2ps`             |

- To preserve space and avoid installing ghc for host until necessary, we provide pre-compiled `Setup.hs` script as `termux-ghc-setup`.
- It can handle `simple`, `configure` and `make` targets. For `custom` target we install ghc for host, compile
  `Setup.hs` with it and make it available as `termux-ghc-setup`.

## Notes:

- Do not use `runhaskell Setup`. All its functionality is made available by `termux-ghc-setup`.
- Same naming scheme is used for ghc tools for on-device build. So, you do not have to handle anything specific for it.
- Currently we have no way to compile packages using `template-haskell`.
