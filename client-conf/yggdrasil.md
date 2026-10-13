## DNS-over-TLS for Yggdrasil (IPv6 only)

**Unbound conf**

```
forward-zone:
    name: "."
    forward-tls-upstream: yes
    # Yggdrasil
    forward-addr: 201:7eab:6f9a:514b:7b8e:f4b1:e376:afd1@853#dot-sg.blahdns.com
    forward-addr: 201:abf1:ba14:9efd:8975:9e9e:9636:786b@853#dot-de.blahdns.com
    
```

**Server IPv6**
```
Singapore: 201:7eab:6f9a:514b:7b8e:f4b1:e376:afd1
Germany: 201:abf1:ba14:9efd:8975:9e9e:9636:786b
```
