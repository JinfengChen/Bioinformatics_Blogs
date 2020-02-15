---
layout: post
title: "HPCC ssh config"
subtitle: 'Config multiple HPCC login for ssh login'
author: "Jinfeng"
header-style: text
tags:
  - Linux
  - HPCC
---

Create a file 'config' in folder '~/.ssh/'. Write the following info in the config file to create a shortcut for each HPCC.

```
Host your_short_cut
HostName your_hpcc_address
User your_user_name
```

Easy login with ssh in terminal

```
ssh pig
```
