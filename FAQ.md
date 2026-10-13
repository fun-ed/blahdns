
## IP / DNS leak test

1. [bash.ws/dnsleak](https://bash.ws/dnsleak)
2. [https://browserleaks.com/ip](https://browserleaks.com/ip)
3. [ipleak.org](https://ipleak.org/)
4. [ipleak.com](http://ipleak.com/full-report)

- [What is my IP](https://ifconfig.co/)
```
curl -4 https://ifconfig.co
curl -6 https://ifconfig.co
```

## Prevent DNS leaking from Chrome browser on Android phone

1. Type `chrome://flags`
2. search for keyword: `async dns`
3. set value to `DISABLED`
4. restart Chrome

<img src="https://github.com/fun-ed/blahdns/raw/master/client-conf/img-source/disable-async-dns-on-android-chrome.jpg" alt="Your image title" width="250"/>


## Troubleshoot

DoH accepts POST requests only (RFC 8484 wire format); GET requests return 403. DoT is served on port 853.

```
// DNS port randomness check
dig +short porttest.dns-oarc.net TXT

// curl with DoH (POST)
printf 'AAABAAABAAAAAAAAA3d3dwdleGFtcGxlA2NvbQAAAQAB' | base64 -d | curl -s -H 'content-type: application/dns-message' --data-binary @- https://doh-de.blahdns.com/dns-query | hexdump -C
printf 'AAABAAABAAAAAAAAA3d3dwdleGFtcGxlA2NvbQAAAQAB' | base64 -d | curl -s -H 'content-type: application/dns-message' --data-binary @- https://doh-sg.blahdns.com/dns-query | hexdump -C

// Kdig on Ubuntu, Debian
apt install knot-dnsutils

// DoT, port 853, with TLS certificate validation
kdig -d @dot-de.blahdns.com +tls-ca +tls-host=dot-de.blahdns.com example.com
kdig -d @dot-sg.blahdns.com +tls-ca +tls-host=dot-sg.blahdns.com example.com

// DoH (POST)
kdig @doh-de.blahdns.com +https=/dns-query example.com

// DoQ, port 784
kdig +quic -p 784 @dot-de.blahdns.com example.com

// Debug DoH with TLS 1.3
openssl s_client -connect doh-de.blahdns.com:443 -servername doh-de.blahdns.com -tls1_3
```

## DNSSEC validation test

1. [https://www.dnssec.cz/](https://www.dnssec.cz/)
2. [https://wander.science/projects/dns/dnssec-resolver-test/](https://wander.science/projects/dns/dnssec-resolver-test/)

Use `dig` to test, this will return with header `AD`

```
dig blahdns.com +dnssec +multi
```

This will failed, should only return a `SERVFAIL`

```
dig www.dnssec-failed.org 

```


## DNS alternative

### Censored DNS
1. https://doh.tiar.app/ (DoT, DoH, Dnscrypt, Singapore)
2. https://doh.dnswarden.com/adblock (DoH, Germany)
3. adblock-dot.dnswarden.com (DoT, Port: 443, 853, Germany)
4. fdns1.dismail.de (DoT, Port: 853, Germany)
5. https://dns.brahma.world/ (DoH, DoT, Plain, Port 853, India)

### Uncensored DNS

1. dns-tls.openbsd.se (DoT)
2. dot1.appliedprivacy.net
3. dns.neutopia.org (DoT)
4. ns1.dnsprivacy.at, ns2.dnsprivacy.at (DoT, Dnscrypt, Port: 853)
5. dns.cmrg.net (DoT, Canada, TCP port: 853 or 443 or 53053)
6. unicast.censurfridns.dk (DoT, Denmark)
7. doh.defaultroutes.de, https://doh.defaultroutes.de/dns-query (DoT, DoH, Port: 853, Germany)

## Server Benchmark
1. [bench.sh](https://cdn.statically.io/gh/teddysun/across/master/bench.sh)
```
// Method 1 ** Recommend 
wget -qO- https://oooo.b-cdn.net/bench.sh | bash

// Method 2
wget -qO- https://cdn.statically.io/gh/teddysun/across/master/bench.sh | bash
```

2. [Unixbench](https://cdn.statically.io/gh/teddysun/across/master/unixbench.sh)
```
// Method 1 ** Recommend 
wget https://oooo.b-cdn.net/unixbench.sh
chmod +x unixbench.sh
./unixbench.sh

// Method 2 (If your server only has IPv6, use Method 1)
wget https://cdn.statically.io/gh/teddysun/across/master/unixbench.sh
chmod +x unixbench.sh
./unixbench.sh
```
1. IPtables DNS DDOs attack: https://github.com/justvanbloom/dns-iptables-rules/blob/master/update_domain_blacklist.sh
Vultr Cloudcompute vs High frequency -- the gist was on the suspended account and is no longer available.
