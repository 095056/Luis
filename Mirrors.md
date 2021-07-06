# Repositories and Mirrors

Termux packages, except bootstrap environment, are served via external web services. There is a primary package server (seed) and number or mirrors, which replicate the content from it to reduce load and provide a some level of redundancy. Mirrors are running either on behalf of maintainers, community members or unaffiliated third parties and are not guaranteed to be always available.

Packages require Termux running on Android 7.0 or higher. Do not try to use repositories listed there on legacy environments.

Service availability may vary depending on your device, Internet connection quality, and censorship events in your country. If we detect serious issue on our side, we will post announce on GitHub and our community pages. Other issues, like introduced on client side or somewhere between endpoints, would be ignored.

## How to use

Run `apt edit-sources`, comment out existing URLs and add line for picked repository, or use the `termux-change-repo` script that is part of the `termux-tools` package.

## Primary host

A default Termux packages repository and content seeder for available mirrors. Server is behind [CloudFlare](https://www.cloudflare.com/) to protect it against DDoS, make it available for IPv4 users (yes, our server is IPv6-only) and provide good download speeds across regions.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://packages.termux.org/apt/termux-main stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://packages.termux.org/apt/termux-games games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://packages.termux.org/apt/termux-root root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://packages.termux.org/apt/termux-science science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://packages.termux.org/apt/termux-unstable unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://packages.termux.org/apt/termux-x11 x11 main`|

Please don't use our host in your forks. Set up your own repository. Otherwise consider to contribute to our project instead of maintaining the custom fork.

## Mirrors

There are listed all known Termux mirrors. If you host a one but didn't find it in the list, please open the issue in https://github.com/termux/termux-packages/issues.

### Mirrors by [a1batross](https://github.com/a1batross)

Updated once per 6 hours.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://termux.mentality.rip/termux-main stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://termux.mentality.rip/termux-games games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://termux.mentality.rip/termux-root root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://termux.mentality.rip/termux-science science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://termux.mentality.rip/termux-unstable unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://termux.mentality.rip/termux-x11 x11 main`|

### Mirrors by [Grimler](https://github.com/grimler91)

Mirrored from the main node, updated once per hour.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://grimler.se/termux-packages-24 stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://grimler.se/game-packages-24 games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://grimler.se/termux-root-packages-24 root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://grimler.se/science-packages-24 science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://grimler.se/unstable-packages unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://grimler.se/x11-packages x11 main`|

### Mirrors by [Kcubeterm](https://github.com/kcubeterm)

Cloned repositories are re-signed by [@kcubeterm's](https://github.com/kcubeterm) key which is missing from `termux-keyring` package version below 1.6.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://dl.kcubeterm.me/termux-packages-24 stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://dl.kcubeterm.me/game-packages-24 games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://dl.kcubeterm.me/termux-root-packages-24 root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://dl.kcubeterm.me/science-packages-24 science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://dl.kcubeterm.me/unstable-packages unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://dl.kcubeterm.me/x11-packages x11 main`|

### Mirrors by [Librehat](https://github.com/librehat)

Updated every 6 hours.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://termux.librehat.com/apt/termux-main stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://termux.librehat.com/apt/termux-games games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://termux.librehat.com/apt/termux-root root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://termux.librehat.com/apt/termux-science science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://termux.librehat.com/apt/termux-unstable unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://termux.librehat.com/apt/termux-x11 x11 main`|

### Mirrors by the [Tsinghua University TUNA Association](https://tuna.moe/)

Mirror for Chinese users for better ping and download speed.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/termux-packages-24/ stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/game-packages-24/ games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/termux-root-packages-24/ root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/science-packages-24/ science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/unstable-packages/ unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/x11-packages/ x11 main`|

### Mirrors by the [Beijing Foreign Studies University](http://www.bfsu.edu.cn/)

Mirror for Chinese users for better ping and download speed.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://mirrors.bfsu.edu.cn/termux/termux-packages-24/ stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://mirrors.bfsu.edu.cn/termux/game-packages-24/ games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://mirrors.bfsu.edu.cn/termux/termux-root-packages-24/ root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://mirrors.bfsu.edu.cn/termux/science-packages-24/ science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://mirrors.bfsu.edu.cn/termux/unstable-packages/ unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://mirrors.bfsu.edu.cn/termux/x11-packages/ x11 main`|

### Mirrors by [University of Science and Technology of China, Linux User Group](https://lug.ustc.edu.cn/)

Mirror for Chinese users for better ping and download speed.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://mirrors.ustc.edu.cn/termux/apt/termux-main/ stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://mirrors.ustc.edu.cn/termux/apt/termux-games/ games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://mirrors.ustc.edu.cn/termux/apt/termux-root/ root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://mirrors.ustc.edu.cn/termux/apt/termux-science/ science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://mirrors.ustc.edu.cn/termux/apt/termux-unstable/ unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://mirrors.ustc.edu.cn/termux/apt/termux-x11/ x11 main`|
