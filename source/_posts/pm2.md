---
title: pm2
date: 2021-06-23 11:48:45
categories:
- manage
version: 
---

## get started

### Start

```bash
# for javascript
pm2 start app.js

# for other script excutable
pm2 start bashscript.sh
pm2 start python-app.py --watch
pm2 start binary-file -- --port 1520
```

### Start Options

```bash
# Specify an app name
--name <app_name>

# Watch and Restart app when files change
--watch

# Set memory threshold for app reload
--max-memory-restart <200MB>

# Specify log file
--log <log_path>

# Pass extra arguments to the script
-- arg1 arg2 arg3

# Delay between automatic restarts
--restart-delay <delay in ms>

# Prefix logs with time
--time

# Do not auto restart app
--no-autorestart

# Specify cron for forced restart
--cron <cron_pattern>

# Attach to application log
--no-daemon
```

### Manage

```bash
# For single process
pm2 [list|ls|status] app_name
pm2 restart app_name
pm2 reload app_name
pm2 stop app_name
pm2 delete app_name

# For processes
# Save the current process list
pm2 dump | save
# Recover
pm2 resurrect
```

### Logs

```bash
pm2 logs <id|name|all> --lines <the number of lines>
```

### Dashboard

```bash
pm2 monit
```