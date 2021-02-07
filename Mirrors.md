## How to use

Open file `$PREFIX/etc/apt/sources.list` or files in `$PREFIX/etc/apt/sources.list.d`, comment out existing URLs and add line for picked mirror, or use the `termux-change-repo` script that is part of the `termux-tools` package.

As of `termux-tools` v0.86, main repository mirrors are being picked and rotated automatically to reduce bandwidth usage on the origin (Bintray).

## Mirrors by [a1batross](https://github.com/a1batross) (OUT-OF-SYNC as of 2021.01.02)

Updated once per 6 hours.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://termux.mentality.rip/termux-packages-24 stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://termux.mentality.rip/game-packages-24 games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://termux.mentality.rip/termux-root-packages-24 root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://termux.mentality.rip/science-packages-24 science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://termux.mentality.rip/unstable-packages unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://termux.mentality.rip/x11-packages x11 main`|

## Mirrors by [Grimler](https://github.com/grimler91)

Updated hourly. Only for installations running Android 7.0 and higher.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://grimler.se/termux-packages-24 stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://grimler.se/game-packages-24 games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://grimler.se/termux-root-packages-24 root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://grimler.se/science-packages-24 science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://grimler.se/unstable-packages unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://grimler.se/x11-packages x11 main`|

## Mirrors by [Xeffyr](https://github.com/xeffyr)

Synchronized manually, update time may vary. Only for installations running Android 7.0 and higher.

Uses [CloudFlare](https://www.cloudflare.com/) CDN to improve download speed and reduce server load as it can provide only
100 mbps. My mirror inaccessible in countries where CloudFlare is blocked, sorry.

`main.termux-mirror.ml` is hosted over IPFS.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://main.termux-mirror.ml stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://games.termux-mirror.ml games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://root.termux-mirror.ml root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://science.termux-mirror.ml science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://unstable.termux-mirror.ml unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://x11.termux-mirror.ml x11 main`|
|[by @its-pointless](https://github.com/its-pointless/its-pointless.github.io)|`deb https://its-pointless.termux-mirror.ml/ termux extras`|

I also provide an unofficial copy of all @termux repositories on my host: https://gitea.warpdestination.ml/termux-mirror

## Mirrors by the [Tsinghua University TUNA Association](https://tuna.moe/)

Mirror for Chinese users for better ping and download speed. Only for Android 7.0 and higher.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/termux-packages-24/ stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/game-packages-24/ games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/termux-root-packages-24/ root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/science-packages-24/ science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/unstable-packages/ unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://mirrors.tuna.tsinghua.edu.cn/termux/x11-packages/ x11 main`|

## Mirrors by the [Beijing Foreign Studies University](http://www.bfsu.edu.cn/)

Mirror for Chinese users for better ping and download speed. Only for Android 7.0 and higher.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://mirrors.bfsu.edu.cn/termux/termux-packages-24/ stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://mirrors.bfsu.edu.cn/termux/game-packages-24/ games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://mirrors.bfsu.edu.cn/termux/termux-root-packages-24/ root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://mirrors.bfsu.edu.cn/termux/science-packages-24/ science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://mirrors.bfsu.edu.cn/termux/unstable-packages/ unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://mirrors.bfsu.edu.cn/termux/x11-packages/ x11 main`|
