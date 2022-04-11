---
title: conda
date: 2021-07-04 12:17:31
categories:
- package
version:
---

## get started

## Env Manage

```bash
conda create --name env_name [[package][=version]]
```

```bash
conda env remove -n env_name
# equivalent to
conda remove -n env_name --all
```
## Package Manage

```bash
conda remove -n env_name package_name
```

## Cache

```bash
# remove index cache, usually done after change channel of .condarc
conda clean -i
```

```bash
# remove package cache
conda clean -p
```