# Mirroring

This page contains suggestions on how to mirror/sync the official repositories, either to create a new, public termux mirror, or just to have a local repository.

## Mirroring with rsync

Per default the repos termux-main, termux-x11, termux-root and termux-main-21 are synced. For personal use it might be sufficient to mirror only the termux-main repo, and in that case you can use the `--exclude` flag to ignore the other repos. Authentication is done with username rsync and password termuxmirror, so to sync all mirrors into a folder `termux` in the local directory, do:

```
RSYNC_PASSWORD=termuxmirror rsync -a --delete rsync@grimler.se::termux termux
```

or to sync all except the termux-main-21 repo (this repo is optional to sync):

```
RSYNC_PASSWORD=termuxmirror rsync -a --delete --exclude termux-main-21 rsync@grimler.se::termux termux
```

## Mirroring with apt-mirror

apt-mirror is a perl script and has a couple of dependencies that need to be installed through cpan or similar. Once installed a config file is needed to select which repos to sync. Here's an example config file that syncs all of termux's repos into `/data/data/com.termux/files/home/termux`:

```
set base_path         /data/data/com.termux/files/home/termux
set mirror_path       $base_path/mirror
set skel_path         $base_path/skel
set var_path          $base_path/var
set postmirror_script $var_path/postmirror.sh
set defaultarch       aarch64
set run_postmirror    0
set nthreads          20
set limit_rate        100m
set _tilde            0
# Use --unlink with wget (for use with hardlinked directories)
set unlink            0
set use_proxy         off
set http_proxy        127.0.0.1:3128
set proxy_user        user
set proxy_password    password

# Main Termux repository
deb-aarch64           https://grimler.se/termux/termux-main stable main
deb-arm               https://grimler.se/termux/termux-main stable main
deb-i686              https://grimler.se/termux/termux-main stable main
deb-x86_64            https://grimler.se/termux/termux-main stable main
clean                 https://grimler.se/termux/termux-main

# root repository
deb-aarch64           https://grimler.se/termux/termux-root root stable
deb-arm               https://grimler.se/termux/termux-root root stable
deb-i686              https://grimler.se/termux/termux-root root stable
deb-x86_64            https://grimler.se/termux/termux-root root stable
clean                 https://grimler.se/termux/termux-root

# x11 repository
deb-aarch64           https://grimler.se/termux/termux-x11 x11 main
deb-arm               https://grimler.se/termux/termux-x11 x11 main
deb-i686              https://grimler.se/termux/termux-x11 x11 main
deb-x86_64            https://grimler.se/termux/termux-x11 x11 main
clean                 https://grimler.se/termux/termux-x11
```

To start the sync you then run `apt-mirror /path/to/termux-config-from-above.list`.

## Mirroring with aptly

Aptly is convenient when dealing with packages and multiple repositories. However, you need to sign the repo with your own gpg key when publishing it, meaning that other people cannot subscribe and use your mirror unless they add your gpg key to apt's trusted keys. Mirroring for personal use works fine though, and can be done through something like:

```
gpg --no-default-keyring --keyring trustedkeys.gpg --recv-keys 5A897D96E57CF20C B0076E490B71616B
aptly mirror create termux-main https://grimler.se/termux/termux-main stable
aptly mirror create termux-root https://grimler.se/termux/termux-root root
aptly mirror create termux-x11 https://grimler.se/termux/termux-x11 x11

aptly mirror update termux-main
aptly mirror update termux-root
aptly mirror update termux-x11

DATE=$(date +%Y%m%d_%H%M)
aptly snapshot create termux-main-$DATE from mirror termux-main
aptly snapshot create termux-root-$DATE from mirror termux-root
aptly snapshot create termux-x11-$DATE from mirror termux-x11

aptly publish snapshot termux-main-$DATE
aptly publish snapshot termux-root-$DATE
aptly publish snapshot termux-x11-$DATE
```

To later update your mirror, repeat all the steps except `aptly mirror create`.

