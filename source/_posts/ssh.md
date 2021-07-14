---
title: ssh
date: 2021-06-27 16:25:26
categories:
- connect
version:
---

## get started

## Forwarding

```bash
# Forward instance's 8080 port to the local machine's 8080 port
# -N disables executing a remote shell
ssh -N -L 8080:127.0.0.1:8080 [user]@<instance-ip>
```