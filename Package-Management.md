Check [Package Management](https://wiki.termux.com/wiki/Package_Management) for more details on managing In-App Termux packages.

Recently Termux moved the main Termux packages hosting from [Bintray to IPFS](https://github.com/termux/termux-packages/issues/6348). This may have created problems for users while running package installation and update commands with `pkg` or `apt`.

If `pkg` or `apt` commands are failing for you, then run `termux-change-repo` and switch to a different [mirror](https://github.com/termux/termux-packages/wiki/Mirrors), specially for the `main` repository. Also make sure your device has internet connectivity and the repository URLs are accessible in a browser. After switching the mirror, optionally run `pkg upgrade` commands to update all packages to the latest available versions if you want.

Changing the mirror may specially be needed if a user is still using `bintray` as the mirror or `pkg upgrade` command hasn't been run in a while to update termux package related scripts.

If you receive errors like `...Release' changed its 'Origin' value from 'Bintray' to...` after changing the mirror, then [accept them](https://github.com/termux/termux-packages/issues/6455).

The URLs changing to weird characters with `ipfs.io`, `10.via0.com` or `dweb.link` as the domain is normal due to IPFS usage.

Note that during certain times of the day, some mirrors may not be available, so either wait or switch to a different mirror.