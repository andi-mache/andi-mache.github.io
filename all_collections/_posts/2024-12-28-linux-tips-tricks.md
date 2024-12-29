---
layout: post
title: linux tips and tricks
date: 2024-12-05
categories: ["DSA", "linux", "arch"]
---


simulate typing on screen
```sh
echo "You can simulate on-screen typing just like in the movies" | pv -qL 10

```


print colors on terminal
```sh
while :; do printf "\e[48;2;$((RANDOM % 256));$((RANDOM % 256));$((RANDOM % 256))m%*s\e[0m" $(tput cols) ""; sleep 0.1; done

```

