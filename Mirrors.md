## How to use

Open file `$PREFIX/etc/apt/sources.list`, comment out existing URLs and add line for picked mirror.
If you are using mirror for non-main repository, make sure that corresponding repository package is
not installed. For example, if you are adding mirror for root packages repository, then you need to
uninstall package `root-repo` to avoid conflicts.

## IPFS

Termux backup mirrors by [@xeffyr](https://github.com/xeffyr). Hosted via IPFS.

1. Main repository:
   ```
   deb https://ipfs.io/ipns/main.termux-ipfs.dynv6.net stable main
   ```

2. Game packages:
   ```
   deb https://ipfs.io/ipns/games.termux-ipfs.dynv6.net games stable
   ```

3. Root packages:
   ```
   deb https://ipfs.io/ipns/root.termux-ipfs.dynv6.net root stable
   ```

4. Science packages:
   ```
   deb https://ipfs.io/ipns/science.termux-ipfs.dynv6.net science stable
   ```

5. Unstable packages:
   ```
   deb https://ipfs.io/ipns/unstable.termux-ipfs.dynv6.net unstable main
   ```

6. X11 packages:
   ```
   deb https://ipfs.io/ipns/x11.termux-ipfs.dynv6.net x11 main
   ```

## Third-party mirrors.

For chinese users:
```
deb https://mirrors.tuna.tsinghua.edu.cn/termux/ stable main
```
Note that it mirrors only legacy repository - https://termux.net.
