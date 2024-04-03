+++
date = "2024-04-03T00:20:39-07:00"
title = "Your python3 install is corrupted. Please fix the '/usr/bin/python3' symlink"
draft = false

tags = ['devops', 'ubuntu', 'do-release-uprade', 'python3', 'corrupted']
+++

On Ubunut, time to time, when running `do-release-upgade` on Python you may got hit with:

```
Your python3 install is corrupted. Please fix the '/usr/bin/python3' symlink.
```

The root cause is the `python3` no longer match the default python version of
the distro. The update progream is part of the distroy, and it requires that same
python version.

Example, your python3 may point to python3.8, where as the current distro
release require python3.6(which is its default python in the apt).

On top of that, `python3` also doesn't like ` /etc/alternatives/python3` when
using with `update-alternative`.

The only way I found to make this move forward is manually set `python3` symlink
to the right python version directly, without going throuh other symlink

Upon that, doing upgrade will work and the side effect of the update is a newer
Python versionfor that distro release is installed and ultimately correct any
python version issue.


```
sudo ln -s /usr/bin/python3.6 /usr/bin/python3
```

If you don't have `python3.6` it can be re-installed:

```
apt install --reinstall python3
# This remove all /etc/alternative/python3 link
update-alternatives --remove-all python3
ln -sf /usr/bin/python3.6 /usr/bin/python3
```

Note, on a good system, this will never happens. This happen when people start
to install python with some third party package or deadsnakes ppa.

Strongly recomend to stay away from that deadsnakes PPA and use `pyenv` tomanage
python version instead.