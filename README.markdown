# Git-Friendly Seafile Syncing Client

Seafile is an open-source cloud storage system.  
Main repository: [haiwen / seafile](https://github.com/haiwen/seafile)

## Background

Several users have reported **Git repository corruption** when syncing repositories with the official Seafile client.
This issue is related to the Seafile client's file monitoring behavior.
It is reproducible (see details [here](https://forum.seafile.com/t/handling-of-git-repositories/266/11)) and can lead to silent data corruption.

At the time of writing, the Seafile development team has indicated that they do not plan to change the current behavior.

Details of the bug and the Seafile maintainers' rationale can be found in the following forum thread:

- [Handling of git repositories](https://forum.seafile.com/t/handling-of-git-repositories)

Relevant GitHub issues:

- [GitHub issue #2677](https://github.com/haiwen/seafile/issues/2677)
- [GitHub issue #2833](https://github.com/haiwen/seafile/issues/2833)

## Purpose

This project modifies the Linux Seafile client to prevent Git repository corruption caused by the client's file monitoring behavior.
**Linux only.**

**Warning:** this repository is not part of the Seafile project.
This is an independent modification originally written for personal use and provided without guarantees.
Use at your own risk and make sure you have backups of your repositories.

## Scope

This modification targets only the `seafile-daemon` component common to the GUI and the command line client on Linux.
No changes are made to the server or to other client components.
The modified `seafile-daemon` is intended to remain compatible with the official Seafile server and clients.

## Installation

A prebuilt Debian package for x86-64 is available: [seafile-daemon_9.0.16+1_amd64.deb](https://ciovil.li/vari/seafile-daemon_9.0.16+1_amd64.deb).

The Seafile client is split into three debian packages: `seafile-cli`, `seafile-gui`, and `seafile-daemon`.
Only the `seafile-daemon` component needs to be updated.
After installation, it is advisable to set `seafile-daemon` on hold; otherwise, `apt` may revert to the official package during upgrades.

To install:

```
sudo dpkg -i seafile-daemon_9.0.16+1_amd64.deb
sudo apt-mark hold seafile-daemon
```

To go back to the version provided by your distribution:

```
sudo dpkg -r --force-depends seafile-daemon
sudo apt install seafile-daemon
```

## License

GPLv2
