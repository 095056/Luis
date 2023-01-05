# Info for mirror maintainers

On `10th` of December `2022` we moved the primary termux packages repository (https://packages.termux.dev) from FossHost to [Hetzner](https://www.hetzner.com/cloud). Now the repository is accessible over both IPv4 and IPv6, and `rsync` can be used to mirror the main repository. The page [How to mirror the official repositories](https://github.com/termux/termux-packages/wiki/How-to-mirror-the-official-repositories) has suggestions for how to mirror our repositories.

The `unstable-packages`, `game-packages` and `science-packages` channels have been merged into the `termux-main` channel and do not need to be synced any longer.

# Repositories and Mirrors

Termux packages, except bootstrap environment, are served via external web services. There is a primary package server (seed) and number or mirrors, which replicate the content from it to reduce load and provide a some level of redundancy. Mirrors are running either on behalf of maintainers, community members or unaffiliated third parties and are not guaranteed to be always available.

Packages require Termux running on Android 7.0 or higher. Do not try to use repositories listed there on legacy environments.

Service availability may vary depending on your device, Internet connection quality, and censorship events in your country. If we detect serious issue on our side, we will post announce on GitHub and our community pages. Other issues, like introduced on client side or somewhere between endpoints, would be ignored.

## How to use

Run `apt edit-sources`, comment out existing URLs and add line for picked repository, or use the `termux-change-repo` script that is part of the `termux-tools` package.

## Primary host

A default Termux packages repository and content seeder for available mirrors.

| Repository                                             | sources.list entry                                            |
|:-------------------------------------------------------|:--------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://packages.termux.dev/apt/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://packages.termux.dev/apt/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://packages.termux.dev/apt/termux-x11 x11 main`     |

CloudFlare CDN endpoint. Fast and stable, but has limits on uploads 100MB max per POST in "free" plan) which makes impossible to use it or submitting packages via GitHub Actions + Aptly REST API.

| Repository                                             | sources.list entry                                               |
|:-------------------------------------------------------|:-----------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://packages-cf.termux.dev/apt/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://packages-cf.termux.dev/apt/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://packages-cf.termux.dev/apt/termux-x11 x11 main`     |

Please don't use our host in termux forks. Set up your own repository. Otherwise consider to contribute to our project instead of maintaining the custom fork.

## Mirrors

There are listed all known Termux mirrors. If you host a one but didn't find it in the list, please open the issue in https://github.com/termux/termux-packages/issues.

### Mirrors that are part of mirror rotation in pkg

These mirrors (listed alphabetically) might be picked, on random, when pkg checks available mirrors and picks one.

#### Mirrors by [a1batross](https://github.com/a1batross)

Updated four times per day.

| Repository                                             | sources.list entry                                         |
|:-------------------------------------------------------|:-----------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://termux.mentality.rip/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://termux.mentality.rip/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://termux.mentality.rip/termux-x11 x11 main`     |

#### Mirrors by [Astra ISP](https://astra.in.ua/)

Updated once per 4 hours.

| Repository                                             | sources.list entry                                           |
|:-------------------------------------------------------|:-------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://termux.astra.in.ua/apt/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://termux.astra.in.ua/apt/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://termux.astra.in.ua/apt/termux-x11 x11 main`     |

#### Mirrors by [DomaiNesia](https://www.domainesia.com/) - Cloud Web Hosting Indonesia Terbaik

Hosted in Jakarta, Indonesia. Updated four times per day.

| Repository                                             | sources.list entry                                                             |
|:-------------------------------------------------------|:-------------------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://linux.domainesia.com/applications/termux/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://linux.domainesia.com/applications/termux/root root stable`        |
| [X11](https://github.com/termux/x11-packages)          | `deb https://linux.domainesia.com/applications/termux/x11 x11 main`            |

#### Mirrors by [Grimler](https://github.com/grimler91)

Mirrored from the main node, updated fairly frequently during "office
hours"

| Repository                                             | sources.list entry                                      |
|:-------------------------------------------------------|:--------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://grimler.se/termux/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://grimler.se/termux/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://grimler.se/termux/termux-x11 x11 main`     |


#### Mirrors by [Librehat](https://github.com/librehat)

Updated four times per day.

| Repository                                             | sources.list entry                                            |
|:-------------------------------------------------------|:--------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://termux.librehat.com/apt/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://termux.librehat.com/apt/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://termux.librehat.com/apt/termux-x11 x11 main`     |

#### Mirrors by [mwt](https://github.com/mwt)

Hosted in East/West coast USA and Europe(via cdn). Updated four times per day.

Check which origin is serving you by checking:
https://mirror.mwt.me/mirror-heartbeat.txt

| Repository                                             | sources.list entry                                  |
|:-------------------------------------------------------|:----------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirror.mwt.me/termux/main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirror.mwt.me/termux/root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirror.mwt.me/termux/x11 x11 main`     |

#### Mirrors by [Nevacloud](https://nevacloud.com/) - Simplified Cloud Servers for Developers

Hosted in Jakarta, Indonesia. Updated four times per day.

| Repository                                             | sources.list entry                                                             |
|:-------------------------------------------------------|:-------------------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirror.nevacloud.com/applications/termux/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirror.nevacloud.com/applications/termux/root root stable`        |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirror.nevacloud.com/applications/termux/x11 x11 main`            |

#### Mirrors by [Purdue University Linux Users Group](https://plug-mirror.rcac.purdue.edu/info.html)

Hosted in Indiana, USA. Updated four times per day.

| Repository                                             | sources.list entry                                                       |
|:-------------------------------------------------------|:-------------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://plug-mirror.rcac.purdue.edu/termux/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://plug-mirror.rcac.purdue.edu/termux/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://plug-mirror.rcac.purdue.edu/termux/termux-x11 x11 main`     |

#### Mirrors by [Computer Science Club of the University of Waterloo](https://csclub.uwaterloo.ca)

Hosted in Canada, Ontario, Waterloo. Updated twice times per day.

| Repository                                             | sources.list entry                                                       |
|:-------------------------------------------------------|:-------------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirror.csclub.uwaterloo.ca/termux/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirror.csclub.uwaterloo.ca/termux/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirror.csclub.uwaterloo.ca/termux/termux-x11 x11 main`     |

#### Mirrors by [Sahilister](https://github.com/sahilister)

Updated four times per day.

| Repository                                             | sources.list entry                                             |
|:-------------------------------------------------------|:---------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirrors.sahilister.in/termux/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirrors.sahilister.in/termux/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirrors.sahilister.in/termux/termux-x11 x11 main`     |

#### Mirrors by [Utermux](https://github.com/utermuxblog)

Hosted in San Jose, California, USA. Updated daily.

More info at https://github.com/UtermuxBlog/Issue.

| Repository                                             | sources.list entry                                               |
|:-------------------------------------------------------|:-----------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirrors.utermux.dev/termux/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirrors.utermux.dev/termux/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirrors.utermux.dev/termux/termux-x11 x11 main`     |

#### Mirrors by [vern.cc](https://vern.cc)

Hosted in New York. Updated once per day.

| Repository                                             | sources.list entry                                          |
|:-------------------------------------------------------|:------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirror.vern.cc/termux/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirror.vern.cc/termux/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirror.vern.cc/termux/termux-x11 x11 main`     |

#### Mirrors by [Fremont Cabal Internet Exchange](https://fcix.net)

Hosted in Fremont, California, USA. Updated every 3 hours. 10Gbps and support IPV4/IPV6.

| Repository                                             | sources.list entry                                          |
|:-------------------------------------------------------|:------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirror.fcix.net/termux/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirror.fcix.net/termux/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirror.fcix.net/termux/termux-x11 x11 main`     |

#### Mirrors by [CyberRex0](https://github.com/cyberrex0)

Hosted in Japan. Updated every 6 hours.

| Repository                                             | sources.list entry                                               |
|:-------------------------------------------------------|:-----------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirrors.cbrx.io/apt/termux/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirrors.cbrx.io/apt/termux/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirrors.cbrx.io/apt/termux/termux-x11 x11 main`     |

#### Mirrors by [Exosunandnet](https://github.com/Exosunandnet)

Hosted in Spain. Updated every 6 hours. 1Gb/s and is IPv4 only.  

| Repository                                             | sources.list entry                                           |
|:-------------------------------------------------------|:-------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://termux.3san.dev/termux/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://termux.3san.dev/termux/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://termux.3san.dev/termux/termux-x11 x11 main`     |

#### Mirrors by [LumitoLuma](https://www.lumito.net)

Hosted in Germany, Updated every an hour.

| Repository                                             | sources.list entry                                               |
|:-------------------------------------------------------|:-----------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://cdn.lumito.net/termux/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://cdn.lumito.net/termux/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://cdn.lumito.net/termux/termux-x11 x11 main`     |

#### Mirrors by [Dev-Nergis](https://github.com/Dev-Nergis)

Hosted in Republic of Korea, Updated every 6 hours.

| Repository                                             | sources.list entry                                               |
|:-------------------------------------------------------|:-----------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirror.textcord.xyz/termux/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirror.textcord.xyz/termux/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirror.textcord.xyz/termux/termux-x11 x11 main`     |

### Mirrors hosted in India

Mirrors for users in India for better ping and download speed.

#### Mirrors by [Nabeelshaikh7](https://github.com/nabeelshaikh7)

This mirror is hosted in India.

| Repository                                             | sources.list entry                                       |
|:-------------------------------------------------------|:---------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://packages.nscdn.top/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://packages.nscdn.top/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://packages.nscdn.top/termux-x11 x11 main`     |

#### Mirrors by [Albonycal](https://github.com/Albonycal)

This mirror is hosted in India, Updated every 53 minutes.

| Repository                                             | sources.list entry                                       |
|:-------------------------------------------------------|:---------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirror.albony.xyz/termux/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirror.albony.xyz/termux/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirror.albony.xyz/termux/termux-x11 x11 main`     |

## Mirrors hosted in Russia

Mirrors for users in Russia for better ping and download speed.

#### Mirrors by [National Research Nuclear University - Moscow Engineering Physics Institute](https://mephi.ru/)

| Repository                                             | sources.list entry                                  |
|:-------------------------------------------------------|:----------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb http://mirror.mephi.ru/termux/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb http://mirror.mephi.ru/termux/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb http://mirror.mephi.ru/termux/termux-x11 x11 main`     |

#### Mirrors by [dmitry](mailto:dmitry@shishkin.email)

Hosted in Nizhny Novgorod, Russia, updated four times per day.

| Repository                                             | sources.list entry                                  |
|:-------------------------------------------------------|:----------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirror.surf/termux/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirror.surf/termux/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirror.surf/termux/termux-x11 x11 main`     |

### Mirrors hosted in Iran

Mirrors for users in Iran for better ping and download speed.

#### Mirrors by [Bardia Moshiri](https://bardia.tech/)

This mirror is hosted in Iran. Updated four times per day.

Rsync: `rsync://mirror.bardia.tech/termux`

Contact: `fakeshell@bardia.tech`

| Repository                                             | sources.list entry                                                          |
|:-------------------------------------------------------|:----------------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirror.bardia.tech/termux/termux-packages-24 stable main`      |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirror.bardia.tech/termux/termux-root-packages-24 root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirror.bardia.tech/termux/x11-packages x11 main`               |

### Mirrors hosted in China

Mirrors for users in China for better ping and download speed.

#### Mirrors by [Beijing Foreign Studies University](http://www.bfsu.edu.cn/)

| Repository                                             | sources.list entry                                                   |
|:-------------------------------------------------------|:---------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirrors.bfsu.edu.cn/termux/apt/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirrors.bfsu.edu.cn/termux/apt/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirrors.bfsu.edu.cn/termux/apt/termux-x11 x11 main`     |

#### Mirrors by [Chongqing University of Posts and Telecommunications](https://www.cqupt.edu.cn/)

More info at https://mirrors.cqupt.edu.cn/.

| Repository                                             | sources.list entry                                                    |
|:-------------------------------------------------------|:----------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirrors.cqupt.edu.cn/termux/apt/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirrors.cqupt.edu.cn/termux/apt/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirrors.cqupt.edu.cn/termux/apt/termux-x11 x11 main`     |

#### Mirrors by [Dongguan University of Technology](https://www.dgut.edu.cn/)

| Repository                                             | sources.list entry                                                   |
|:-------------------------------------------------------|:---------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirrors.dgut.edu.cn/termux/apt/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirrors.dgut.edu.cn/termux/apt/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirrors.dgut.edu.cn/termux/apt/termux-x11 x11 main`     |

#### Mirrors by [Harbin Institute of Technology](https://www.hit.edu.cn/)

| Repository                                             | sources.list entry                                                  |
|:-------------------------------------------------------|:--------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirrors.hit.edu.cn/termux/apt/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirrors.hit.edu.cn/termux/apt/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirrors.hit.edu.cn/termux/apt/termux-x11 x11 main`     |

#### Mirrors by [Nanjing University of Posts and Telecommunications](https://mirrors.njupt.edu.cn/)

| Repository                                             | sources.list entry                                                   |
|:-------------------------------------------------------|:---------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirrors.njupt.edu.cn/termux/apt/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirrors.njupt.edu.cn/termux/apt/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirrors.njupt.edu.cn/termux/apt/termux-x11 x11 main`     |

#### Mirrors by [Nanyang Institute of Technology](https://mirror.nyist.edu.cn/)

| Repository                                             | sources.list entry                                                   |
|:-------------------------------------------------------|:---------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirror.nyist.edu.cn/termux/apt/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirror.nyist.edu.cn/termux/apt/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirror.nyist.edu.cn/termux/apt/termux-x11 x11 main`     |

#### Mirrors by [eScience Center, Nanjing University](https://www.nju.edu.cn/)

| Repository                                             | sources.list entry                                                 |
|:-------------------------------------------------------|:-------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirror.nju.edu.cn/termux/apt/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirror.nju.edu.cn/termux/apt/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirror.nju.edu.cn/termux/apt/termux-x11 x11 main`     |

#### Mirrors by [Shandong University](https://mirrors.sdu.edu.cn/)

| Repository                                             | sources.list entry                                              |
|:-------------------------------------------------------|:----------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirrors.sdu.edu.cn/termux/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirrors.sdu.edu.cn/termux/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirrors.sdu.edu.cn/termux/termux-x11 x11 main`     |

#### Mirrors by [Shenyang Aerospace University](https://mirrors.sau.edu.cn/)

| Repository                                             | sources.list entry                                                  |
|:-------------------------------------------------------|:--------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirrors.sau.edu.cn/termux/apt/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirrors.sau.edu.cn/termux/apt/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirrors.sau.edu.cn/termux/apt/termux-x11 x11 main`     |

#### Mirrors by [South China Agricultural University](https://mirrors.scau.edu.cn/)

| Repository                                             | sources.list entry                                                   |
|:-------------------------------------------------------|:---------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirrors.scau.edu.cn/termux/apt/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirrors.scau.edu.cn/termux/apt/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirrors.scau.edu.cn/termux/apt/termux-x11 x11 main`     |


#### Mirrors by [Southern University of Science and Technology](https://mirrors.sustech.edu.cn/)

| Repository                                             | sources.list entry                                                      |
|:-------------------------------------------------------|:------------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirrors.sustech.edu.cn/termux/apt/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirrors.sustech.edu.cn/termux/apt/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirrors.sustech.edu.cn/termux/apt/termux-x11 x11 main`     |

#### Mirrors by [Tsinghua University TUNA Association](https://tuna.moe/)

| Repository                                             | sources.list entry                                                            |
|:-------------------------------------------------------|:------------------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirrors.tuna.tsinghua.edu.cn/termux/apt/termux-main stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirrors.tuna.tsinghua.edu.cn/termux/apt/termux-root root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirrors.tuna.tsinghua.edu.cn/termux/apt/termux-x11 x11 main`     |

#### Mirrors by [Peking University](https://www.pku.edu.cn/)

| Repository                                             | sources.list entry                                                    |
|:-------------------------------------------------------|:----------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirrors.pku.edu.cn/termux/termux-main/ stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirrors.pku.edu.cn/termux/termux-root/ root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirrors.pku.edu.cn/termux/termux-x11/ x11 main`     |

#### Mirrors by [University of Science and Technology of China, Linux User Group](https://lug.ustc.edu.cn/)

| Repository                                             | sources.list entry                                                    |
|:-------------------------------------------------------|:----------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirrors.ustc.edu.cn/termux/apt/termux-main/ stable main` |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirrors.ustc.edu.cn/termux/apt/termux-root/ root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirrors.ustc.edu.cn/termux/apt/termux-x11/ x11 main`     |

#### Mirrors by [Alibaba Open Source Mirror Site](https://mirrors.aliyun.com/)

More info at https://mirrors.aliyun.com/about.

| Repository                                             | sources.list entry                                                          |
|:-------------------------------------------------------|:----------------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirrors.aliyun.com/termux/termux-packages-24 stable main`      |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirrors.aliyun.com/termux/termux-root-packages-24 root stable` |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirrors.aliyun.com/termux/x11-packages x11 main`               |

#### Mirrors by [ISCAS - Institute of Software, Chinese Academy of Sciences](https://isrc.iscas.ac.cn/)

| Repository                                             | sources.list entry                                                          |
|:-------------------------------------------------------|:----------------------------------------------------------------------------|
| [Main](https://github.com/termux/termux-packages)      | `deb https://mirror.iscas.ac.cn/termux/apt/termux-main/ stable main`        |
| [Root](https://github.com/termux/termux-root-packages) | `deb https://mirror.iscas.ac.cn/termux/apt/termux-root/ root stable`        |
| [X11](https://github.com/termux/x11-packages)          | `deb https://mirror.iscas.ac.cn/termux/apt/termux-x11/ x11 main`            |
