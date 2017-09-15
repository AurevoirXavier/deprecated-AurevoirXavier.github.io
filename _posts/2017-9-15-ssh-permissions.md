---
layout: post
title: "SSH permissions"
date:   2017-09-15
excerpt: "ssh 权限"
tags: [Linux, OSX, ssh]
comments: true
---

The following permissions are needed:

- The `.ssh` folder: `700 (drwx------)`
- The public key: `644 (-rw-r--r--)`
- The private key: `600 (-rw-------)`

Also:

```Shell
chmod g-w ~/
chmod o-wx ~/
```

