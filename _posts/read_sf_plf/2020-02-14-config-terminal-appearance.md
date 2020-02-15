---
layout: post
title: "Config terminal appearance"
subtitle: 'Make your HPCC all same style'
author: "Jinfeng"
header-style: text
lang: en
tags:
  - Linux
---

In HPCC, add the following line in '~/.Xdefaults' to config color, font of ssh terminal. 

```
xterm*background: black
xterm*foreground: white
xterm*font:             -misc-fixed-medium-*-*-*-*-140-*-*-*-100-*-*

*VT100.Translations: #override \
              <Key>BackSpace: string(0x7F)\n\
              <Key>Delete:    string("\033[3~")\n\
              <Key>Home:      string("\033[1~")\n\
              <Key>End:       string("\033[4~")
*ttyModes: erase ^? 
```
