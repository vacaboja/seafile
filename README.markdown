# Git-Friendly Seafile Syncing Client

Seafile is an open-source cloud storage system.  
Main repository: [haiwen / seafile](https://github.com/haiwen/seafile)

## Background

Several users have reported **Git repository corruption** when syncing repositories with the official Seafile client. Relevant discussions:

- [Handling of git repositories](https://forum.seafile.com/t/handling-of-git-repositories)
- [GitHub issue #2677](https://github.com/haiwen/seafile/issues/2677)
- [GitHub issue #2833](https://github.com/haiwen/seafile/issues/2833)

At the time of writing, this issue is considered low priority by the Seafile development team.

## Purpose

This project provides a **tentative workaround** for the Git corruption issue by offering a modified Seafile syncing client. **Linux only.**

**Warning:** this workaround is not officially supported by the Seafile project.

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

## Status

This is a temporary solution while waiting for an official fix upstream.  
Use at your own risk and make sure you have backups of your repositories.

## License

GPLv2
