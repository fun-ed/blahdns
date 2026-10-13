## DNS-over-TLS for Yggdrasil (IPv6 only)

**Unbound conf**

```
forward-zone:
    name: "."
    forward-tls-upstream: yes
    # Yggdrasil
    forward-addr: 201:d0be:9b34:c3d1:23e3:2fab:58c8:ce40@853#dot-sg.blahdns.com
    forward-addr: 201:abf1:ba14:9efd:8975:9e9e:9636:786b@853#dot-de.blahdns.com
    
```

**Server IPv6**
```
Singapore: 201:d0be:9b34:c3d1:23e3:2fab:58c8:ce40
Germany: 201:abf1:ba14:9efd:8975:9e9e:9636:786b
```
