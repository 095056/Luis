This page describes the thoughts behind how debs are uploaded from github actions to the repository hosted at grimler.se

# Overall goals

* Automatic uploading of built debs from github actions to self-hosted repository

* Sorting debs and signing of repository should be handled automatically on the server

* Decrease the amount of damage malicious use of the github actions system could do

#  Short summary of design

There are three relevant users:

* "termuxdebs" whose only purpose is to receive archive with built debs from github actions

* "termuxsigner" who looks for new files, parses them to move debs to the right place and then rebuilds repository metadata files

* "httpd" who serves the repository to visitors

General security advice:

* ssh access with password authentication is disabled

* a firewall is running with a minimal number of open ports

* passwords for users and root are unique and stored with a password manager

## termuxdebs user

termuxdebs user is only accessible over sftp and jailed to a single directory. The private ssh key for accessing termuxdebs is stored as
a github secret. It is (unfortunately) not password protected. A dedicated sshd instance is used for the sftp access for termuxdebs. termuxdebs default shell is set to restricted bash (rbash), with PATH unset in .profile. The directory where files are uploaded is owned by
termuxdebs:termux where termux is a group that both termuxdebs and termuxsigner belongs to. The groups has rx rights, while the termuxdebs user has rwx rights.

## termuxsigner user

To detect uploaded files an incron job is running for termuxsigner. **NOTE: incron is no longer developed and have some security issues**, see github page: https://github.com/ar-/incron.

On an `IN_WRITE_CLOSE` event a script `add-termux-deb.sh` is run with the new file as an argument. The full incron job looks like

```
path-to-jail	IN_CLOSE_WRITE	/usr/bin/add-termux-deb.sh $@/$#
```

where `$@/$#` expands to the full path to the new file in path-to-jail/. Note that add-termux-deb.sh must have the .sh suffix, or a prefixed /bin/bash, incron does not respect shebangs.


The script gets the repository name from the filename, extracts the archive, and then loops over known arches and parses deb archives if they exist.

The debs are put into the right arch folder in the right repo, apt-ftparchive is used to re-create the Packages file for each arch and then to create a new Release file. Thereafter the repository is signed with gpg. The gpg private key used for signing the repository in termuxsigner's home directory. It is (unfortunately) not password protected.

The repository ends up owned by termuxsigner:termuxsigner, and the httpd (and termuxdebs) users only have rx rights on the files.

## httpd user

How the repository will not be covered here as there is nothing special about the setup really.
