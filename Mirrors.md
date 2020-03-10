## How to use

Open file `$PREFIX/etc/apt/sources.list` or files in `$PREFIX/etc/apt/sources.list.d`, comment out existing URLs and add line for picked mirror.

## Mirrors by [Xeffyr](https://github.com/xeffyr)

Updated daily. Only for installations running Android 7.0 and higher.

*Measures against crawlers are activated*.

Main ([termux-packages](https://github.com/termux/termux-packages)):
```
deb https://main.termux-mirror.ml stable main
```

Games ([game-packages](https://github.com/termux/game-packages)):
```
deb https://games.termux-mirror.ml games stable
```

Root ([termux-root-packages](https://github.com/termux/termux-root-packages)):
```
deb https://root.termux-mirror.ml root stable
```

Science ([science-packages](https://github.com/termux/science-packages)):
```
deb https://science.termux-mirror.ml science stable
```

Unstable ([unstable-packages](https://github.com/termux/unstable-packages)):
```
deb https://unstable.termux-mirror.ml unstable main
```

X11 ([x11-packages](https://github.com/termux/x11-packages)):
```
deb https://x11.termux-mirror.ml x11 main
```

## Third-party mirrors.

For chinese users:
```
deb https://mirrors.tuna.tsinghua.edu.cn/termux/ stable main
```
\- compatible only with devices running Android 7 or higher.