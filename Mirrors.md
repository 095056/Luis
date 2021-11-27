# Info for mirror maintainers

unstable-packages and game-packages have been merged into the main (termux-packages) repositories. There's no need to sync them anymore, and  they can be removed completely in (for example) March 2022. This gives users time to upgrade there packages before, so that the removal does not cause any problems.

# Repositories and Mirrors

Termux packages, except bootstrap environment, are served via external web services. There is a primary package server (seed) and number or mirrors, which replicate the content from it to reduce load and provide a some level of redundancy. Mirrors are running either on behalf of maintainers, community members or unaffiliated third parties and are not guaranteed to be always available.

Packages require Termux running on Android 7.0 or higher. Do not try to use repositories listed there on legacy environments.

Service availability may vary depending on your device, Internet connection quality, and censorship events in your country. If we detect serious issue on our side, we will post announce on GitHub and our community pages. Other issues, like introduced on client side or somewhere between endpoints, would be ignored.

## How to use

Run `apt edit-sources`, comment out existing URLs and add line for picked repository, or use the `termux-change-repo` script that is part of the `termux-tools` package.

## Primary host

A default Termux packages repository and content seeder for available mirrors. Server is provided for free by [FossHost](https://fosshost.org/) - a hosting provider for open source communities.

**Server is IPv6-only and uses IPv6-to-IPv4 proxy, also provided by FossHost. It is quite slow but we don't have anything better at the moment. Hopefully you understand what's going on. If slow download speed bothers you, please use mirror instead.**

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://packages.termux.org/apt/termux-main stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://packages.termux.org/apt/termux-games games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://packages.termux.org/apt/termux-root root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://packages.termux.org/apt/termux-science science stable`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://packages.termux.org/apt/termux-x11 x11 main`|

CloudFlare CDN endpoint. Fast and stable, but has limits on uploads (100MB max per POST in "free" plan) which makes impossible to use it for submitting packages via GitHub Actions + Aptly REST API.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://packages-cf.termux.org/apt/termux-main stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://packages-cf.termux.org/apt/termux-games games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://packages-cf.termux.org/apt/termux-root root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://packages-cf.termux.org/apt/termux-science science stable`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://packages-cf.termux.org/apt/termux-x11 x11 main`|

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
|[X11](https://github.com/termux/x11-packages)       |`deb https://termux.mentality.rip/termux-x11 x11 main`|

### Mirrors by [Astra ISP](https://astra.in.ua/)

Updated once per 4 hours.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://termux.astra.in.ua/apt/termux-main stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://termux.astra.in.ua/apt/termux-games games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://termux.astra.in.ua/apt/termux-root root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://termux.astra.in.ua/apt/termux-science science stable`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://termux.astra.in.ua/apt/termux-x11 x11 main`|

### Mirrors by [Bardia Moshiri](https://bardia.tech/)

This mirror is hosted in Iran. Syncing every 6 hours.

Rsync: `rsync://mirror.bardia.tech/termux`

Contact: `fakeshell@bardia.tech`

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://mirror.bardia.tech/termux/termux-packages-24/ stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://mirror.bardia.tech/termux/game-packages-24/ games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://mirror.bardia.tech/termux/termux-root-packages-24/ root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://mirror.bardia.tech/termux/science-packages-24/ science stable`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://mirror.bardia.tech/termux/x11-packages/ x11 main`|

### Mirrors by [Grimler](https://github.com/grimler91)

Mirrored from the main node, updated hourly during "office hours" (requires a gpg hardware key to be accessible for repo signing to work).

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://grimler.se/termux-packages-24 stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://grimler.se/game-packages-24 games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://grimler.se/termux-root-packages-24 root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://grimler.se/science-packages-24 science stable`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://grimler.se/x11-packages x11 main`|

### Mirrors by [Librehat](https://github.com/librehat)

Updated every 6 hours.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://termux.librehat.com/apt/termux-main stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://termux.librehat.com/apt/termux-games games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://termux.librehat.com/apt/termux-root root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://termux.librehat.com/apt/termux-science science stable`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://termux.librehat.com/apt/termux-x11 x11 main`|

### Mirrors by the [Tsinghua University TUNA Association](https://tuna.moe/)

Mirror for Chinese users for better ping and download speed.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/apt/termux-main stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/apt/termux-games games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/apt/termux-root root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/apt/termux-science science stable`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/apt/termux-x11 x11 main`|

### Mirrors by the [Beijing Foreign Studies University](http://www.bfsu.edu.cn/)

Mirror for Chinese users for better ping and download speed.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://mirrors.bfsu.edu.cn/termux/apt/termux-main stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://mirrors.bfsu.edu.cn/termux/apt/termux-games games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://mirrors.bfsu.edu.cn/termux/apt/termux-root root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://mirrors.bfsu.edu.cn/termux/apt/termux-science science stable`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://mirrors.bfsu.edu.cn/termux/apt/termux-x11 x11 main`|

### Mirrors by [University of Science and Technology of China, Linux User Group](https://lug.ustc.edu.cn/)

Mirror for Chinese users for better ping and download speed.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://mirrors.ustc.edu.cn/termux/apt/termux-main/ stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://mirrors.ustc.edu.cn/termux/apt/termux-games/ games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://mirrors.ustc.edu.cn/termux/apt/termux-root/ root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://mirrors.ustc.edu.cn/termux/apt/termux-science/ science stable`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://mirrors.ustc.edu.cn/termux/apt/termux-x11/ x11 main`|

### Mirrors by [eScience Center, Nanjing University](https://www.nju.edu.cn/)

Mirror for Chinese users for better ping and download speed.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://mirror.nju.edu.cn/termux/apt/termux-main stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://mirror.nju.edu.cn/termux/apt/termux-games games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://mirror.nju.edu.cn/termux/apt/termux-root root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://mirror.nju.edu.cn/termux/apt/termux-science science stable`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://mirror.nju.edu.cn/termux/apt/termux-x11 x11 main`|