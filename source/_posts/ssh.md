---
title: ssh
date: 2021-06-27 16:25:26
categories:
- basic
version:
---

## get started

## Connect

```bash
# connect according to config
ssh [host]
# custom username or port
ssh -p [port] [user]@<instance-ip>
# X11 forwarding
ssh -X [host]
# X11 forwarding without securing
ssh -Y [host]
```

## Port Forwarding

```bash
# Forward instance's 8080 port to the local machine's 8080 port
# -N disables executing a remote shell, making it just forwarding
ssh -N -L 8080:127.0.0.1:8080 [user]@<instance-ip>
```

## Configuration

```txt
Host *

    # X related
    XAuthLocation /usr/X11/bin/xauth

    # Connection Keep Alive
    ServerAliveInterval 60
    ServerAliveCountMax 5

    # Multiplexing/ControlPersist
    ControlMaster auto
    ControlPath ~/.ssh/%r@%h:%p.socket
    ControlPersist 10m

Host example-host
  HostName 8.8.8.8
  Port 22
  User google
  ProxyCommand nc -X 5 -x 127.0.0.1:7890 %h %p
```