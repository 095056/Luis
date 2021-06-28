There are listed all known Termux mirrors. If you host a one but didn't find it in the list, please open the issue in https://github.com/termux/termux-packages/issues.

Mirrors listed there are expected to be compatible with the latest Termux version, i.e. they are only for Termux running on Android 7.0+.

## How to use

Run `apt edit-sources`, comment out existing URLs and add line for picked mirror, or use the `termux-change-repo` script that is part of the `termux-tools` package.

## Mirrors by [a1batross](https://github.com/a1batross)

Updated once per 6 hours.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://termux.mentality.rip/termux-main stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://termux.mentality.rip/termux-games games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://termux.mentality.rip/termux-root root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://termux.mentality.rip/termux-science science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://termux.mentality.rip/termux-unstable unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://termux.mentality.rip/termux-x11 x11 main`|

## Mirrors by [Grimler](https://github.com/grimler91)

Mirrored from the main node, updated once per hour.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://grimler.se/termux-packages-24 stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://grimler.se/game-packages-24 games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://grimler.se/termux-root-packages-24 root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://grimler.se/science-packages-24 science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://grimler.se/unstable-packages unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://grimler.se/x11-packages x11 main`|

## Mirrors by [Kcubeterm](https://github.com/kcubeterm)

Cloned repositories are re-signed by [@kcubeterm's](https://github.com/kcubeterm) key which is missing from `termux-keyring` package version below 1.6.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://dl.kcubeterm.me/termux-packages-24 stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://dl.kcubeterm.me/game-packages-24 games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://dl.kcubeterm.me/termux-root-packages-24 root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://dl.kcubeterm.me/science-packages-24 science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://dl.kcubeterm.me/unstable-packages unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://dl.kcubeterm.me/x11-packages x11 main`|

## Mirrors by [librehat](https://github.com/librehat)

Updated every 6 hours.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://termux.librehat.com/apt/termux-main stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://termux.librehat.com/apt/termux-games games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://termux.librehat.com/apt/termux-root root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://termux.librehat.com/apt/termux-science science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://termux.librehat.com/apt/termux-unstable unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://termux.librehat.com/apt/termux-x11 x11 main`|

## Mirrors by the [Tsinghua University TUNA Association](https://tuna.moe/)

Mirror for Chinese users for better ping and download speed.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/termux-packages-24/ stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/game-packages-24/ games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/termux-root-packages-24/ root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/science-packages-24/ science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/unstable-packages/ unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/x11-packages/ x11 main`|

## Mirrors by the [Beijing Foreign Studies University](http://www.bfsu.edu.cn/)

Mirror for Chinese users for better ping and download speed.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://mirrors.bfsu.edu.cn/termux/termux-packages-24/ stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://mirrors.bfsu.edu.cn/termux/game-packages-24/ games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://mirrors.bfsu.edu.cn/termux/termux-root-packages-24/ root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://mirrors.bfsu.edu.cn/termux/science-packages-24/ science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://mirrors.bfsu.edu.cn/termux/unstable-packages/ unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://mirrors.bfsu.edu.cn/termux/x11-packages/ x11 main`|

## Mirrors by [University of Science and Technology of China, Linux User Group](https://lug.ustc.edu.cn/)

Mirror for Chinese users for better ping and download speed.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://mirrors.ustc.edu.cn/termux/apt/termux-main/ stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://mirrors.ustc.edu.cn/termux/apt/termux-games/ games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://mirrors.ustc.edu.cn/termux/apt/termux-root/ root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://mirrors.ustc.edu.cn/termux/apt/termux-science/ science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://mirrors.ustc.edu.cn/termux/apt/termux-unstable/ unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://mirrors.ustc.edu.cn/termux/apt/termux-x11/ x11 main`|
