+++
date = "2023-08-13T23:16:41-07:00"
title = "how to clear journalctl systemd log"
draft = true

tags = []
+++

journalctl --vacuum-time=2d
Retain only the past 500 MB:

journalctl --vacuum-size=500M