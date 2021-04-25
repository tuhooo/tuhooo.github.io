---
layout: post
title: "Linux config TMOUT"
category: linux
---





Linux config `TMOUT`.



TMOUT: time out, I think it means this.



write this in `/etc/profile`

```
export TMOUT=0
readonly TMOUT
```



* 0: never time out
* readonly: you can not change this



After I set ssh keepalive correctly, bu terminal still disconnects with server.

So we have to set up this config.