---
title: Quick Build Guide
description: "How to build the libptpmgmt library and what you can do with its make file."
---

# _GNU build_
We use GNU build.

`autoconf`

`./configure`

`make`

---

# _configure_

The `configure` script support options.  

Some basic options come from `autoconf` and some are specific to our project.  

Use `help` to see more information:

`./configure --help`

---

# _Make file_
The `make` file has many targets and parameters.  

Use help to see more information:

`make help`

---

# _Linux distribution_

We provide libraries and wrapper libraries for scripting. You can generate packages for installation.  

For Debian and Ubuntu packages:

`make deb`

For Red Hat packages (RPM):

`make rpm`

For Arch Linux packages:

`make pkg`

To install on Gentoo:

`make gentoo`