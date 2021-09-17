---
title: "lima-vm resolv.conf"
date: 2021-09-17T18:00:30+09:00
categories:
  - blog
  - docker
tags:
  - tech
  - lima-vm
---

From newer ubuntu cannot resolve ".local" domain w/ default resolv.conf.
Then here is the [lima-vm]'s configuration, I wrote. (too long, so just "provision" part only.)

```yaml
provision:
  - mode: system
    script: |
      #!/bin/bash
      set -eux -o pipefail
      sed -i"" -e "s/.*DNSStubListener=yes/DNSStubListener=no/" /etc/systemd/resolved.conf
      ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf
      systemctl restart systemd-resolved
```

[lima-vm]: https://github.com/lima-vm/lima
