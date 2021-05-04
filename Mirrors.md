## How to use

Run `apt edit-sources`, comment out existing URLs and add line for picked mirror, or use the `termux-change-repo` script that is part of the `termux-tools` package.

## Mirrors by [a1batross](https://github.com/a1batross)

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

Mirrors for termux-packages, game-packages, science-packages and termux-root-packages are updated directly from github actions.

**NOTE:** due to the current github action build issues the repos are a bit behind.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://grimler.se/termux-packages-24 stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://grimler.se/game-packages-24 games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://grimler.se/termux-root-packages-24 root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://grimler.se/science-packages-24 science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://grimler.se/unstable-packages unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://grimler.se/x11-packages x11 main`|

## Mirrors by [Xeffyr](https://github.com/xeffyr)

Only for installations running Android 7.0 and higher.

Uses IPFS for sole purpose of delegating repository hosting to "free" high performance hosts (aka "IPFS gateways"). Decentralization and persistence are not taken into account.

Also:
* Mirror is updated manually to ensure stability and gateway caching efficiency.
* Mirror does not keep track of older package versions to optimize disk space usage.
* Primary node can be shutdown during night times (22:00 - 09:00 UTC).

Recommended IPFS gateways are:
* `ipfs.io`
* `10.via0.com`
* `dweb.link`

You can try other gateways listed on https://ipfs.github.io/public-gateway-checker/ or even setup your own.

|Repository|sources.list entry                                               |
|:---------|:----------------------------------------------------------------|
|[Main](https://github.com/termux/termux-packages)      |`deb https://ipfs.io/ipns/k51qzi5uqu5dg9vawh923wejqffxiu9bhqlze5f508msk0h7ylpac27fdgaskx stable main`|
|[Games](https://github.com/termux/game-packages)     |`deb https://ipfs.io/ipns/k51qzi5uqu5dhngjg68o8x9uimwy5h8iqt91n2266idc7uet9ew3lc472upy27 games stable` |
|[Root](https://github.com/termux/termux-root-packages)      |`deb https://ipfs.io/ipns/k51qzi5uqu5dlp5yjlahzcp3kfpnhbifo9ka9iybo3bp5vt781duafkyyvt9al root stable`|
|[Science](https://github.com/termux/science-packages)   |`deb https://ipfs.io/ipns/k51qzi5uqu5dhvbtvdf46kkhobzgamhiirte6s6k28l2c1iapumphh3cpkw33f science stable`|
|[Unstable](https://github.com/termux/unstable-packages)  |`deb https://ipfs.io/ipns/k51qzi5uqu5dj05z8mr958kwvrg7a0wqouj5nnoo5uqu1btnsljvpznfaav9nk unstable main`|
|[X11](https://github.com/termux/x11-packages)       |`deb https://ipfs.io/ipns/k51qzi5uqu5dgu3homski160l4t4bmp52vb6dbgxb5bda90rewnwg64wnkwxj4 x11 main`|

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
