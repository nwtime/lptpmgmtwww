---
title: "clkmgr_proxy: Clock Manager proxy service"
description: "The Clock Manager proxy service interacts with clock synchronization services to obtain real-time synchronization
status, filtering and extracting synchronization data, passing it to the Clock Manager client applications via message queue IPC."
date: 2025-08-13 
---

### clkmgr_proxy: Clock Manager proxy service

#### SYNOPSIS

<code>clkmgr_proxy [ OPTIONS ] [ -f FILE ]</code>

#### DESCRIPTION

The Clock Manager proxy service interacts with clock synchronization services like [ptp4l(8)](https://linuxptp.nwtime.org/documentation/ptp4l/) and 
[chronyd(8)](https://chrony-project.org/doc/4.8/chronyd.html) to obtain real-time synchronization status, filtering and extracting synchronization 
data, and passing it to the Clock Manager client applications via message queue IPC. Clock synchronization monitoring is complex due to the need 
for multiple synchronization services to discipline system time with GM time, further compounded by PTP multidomain and multiple time bases. The 
proxy service resolves this issue by consolidating all synchronization information, allowing client applications to simply communicate with the 
proxy service for seamless integration and avoiding licensing complications. The proxy service can be configured using a JSON configuration file, 
as described in [clkmgr_proxy_cfg(5)](/documentation/man/clkmgr_proxy_cfg/).

#### OPTIONS

<code>**-f [file]**</code>

: Read configuration from _file_.

<code>**-a 0|1**</code>

: Open message queue in access all mode.
  * 0: disable (default)
  * 1: enable

<code>**-l lvl**</code>

: Set log level.
  * 0: ERROR
  * 1:  INFO (default)
  * 2: DEBUG
  * 3: TRACE

<code>**-q 0|1**</code>

: Enable or disable quiet mode.
  * 0: disable
  * 1: enable
  
<code>**-s 0|1**</code>

: Enable or disable use of system logging.
  * 0: disable
  * 1: enable

<code>**-v**</code>

: Show version.

<code>**-h**</code>

: Show help message.

#### SEE ALSO
[clkmgr_proxy_cfg(5)](/documentation/man/clkmgr_proxy_cfg/)