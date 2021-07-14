---
title: proxy
date: 2021-07-04 12:14:36
categories:
- connect
version:
---

## get started

### Terminal

```bash
export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7890
```

### Git

```bash
# For all the connections
# just by setting http proxy can git clone through https connection
git config --global http.proxy socks5://127.0.0.1:1080
git config --global --unset http.proxy
# For specific git server
git config --global http.https://github.com.proxy socks5://127.0.0.1:1080
git config --global --unset http.https://github.com.proxy
```