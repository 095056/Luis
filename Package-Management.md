# Package Management

Check [Package Management Wiki Page](https://wiki.termux.com/wiki/Package_Management) for more details on managing In-App Termux packages.

### Package Command Errors

Recently Termux moved the primary Termux package repository hosting from [**Bintray to IPFS**](https://github.com/termux/termux-packages/issues/6348) since [**Bintray has shut down on May 1st, 2021**](https://jfrog.com/blog/into-the-sunset-bintray-jcenter-gocenter-and-chartcenter/). This has created problems for users while running package installation and update commands with `pkg` or `apt` and their commands will fail with errors similar to following.

```
E: The repository 'https://termux.org/packages stable Release' does no longer have a Release file.
N: Metadata integrity can't be verified, repository is disabled now.
N: Possible cause: repository is under maintenance or down (wrong sources.list URL?).
```

```
E: The repository 'https://dl.bintray.com/grimler/game-packages-24 games Release' does not have a Release file.
N: Metadata integrity can't be verified, repository is disabled now.
N: Possible cause: repository is under maintenance or down (wrong sources.list URL?).
```

```
E: The repository 'https://science.termux-mirror.ml science Release' does not have a Release file.
N: Metadata integrity can't be verified, repository is disabled now.
N: Possible cause: repository is under maintenance or down (wrong sources.list URL?).
```

If that is the case, then run `termux-change-repo` command and **change your mirror** [mirror](https://github.com/termux/termux-packages/wiki/Mirrors) for the `main` repository. If you have installed other [package repositories](https://github.com/termux/termux-packages/wiki#packages), like `science`, `games` and `unstable`, then you **must** select and change those mirrors as well. You can check your current mirrors by running the `termux-info` command.

After changing the mirror, optionally run `pkg upgrade` command to update all packages to the latest available versions if you want, or at least update `termux-tools` package with `pkg install termux-tools` command. Also make sure your device has internet connectivity and the repository URLs are accessible in a browser.

You can check this [**video**](https://user-images.githubusercontent.com/25881154/116244521-ad43a780-a770-11eb-88c6-054fb1950bfd.mp4) for how to change the mirrors.

Changing the mirror may specially be needed if a user is still using `bintray` as the mirror or `pkg upgrade` command hasn't been run in a while to update termux package related scripts.

If you receive errors like `...Release' changed its 'Origin' value from 'Bintray' to...` after changing the mirror, then [accept them](https://github.com/termux/termux-packages/issues/6455).

The URLs changing to weird characters with `ipfs.io`, `10.via0.com` or `dweb.link` as the domain is normal due to IPFS usage.

Note that during certain times of the day, some mirrors like [xeffys's](https://github.com/termux/termux-packages/wiki/Mirrors#mirrors-by-xeffyr) may not be available, so either wait or change to a different mirror.

