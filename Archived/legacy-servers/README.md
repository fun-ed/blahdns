# Retired servers (Japan, Finland, Switzerland)

Japan, Switzerland and Finland were discontinued on 2024-07-15. The configuration below was moved here from the active docs on 2026-10-14 for reference only; these hosts and IPs no longer serve BlahDNS.
Some snippets also show former Singapore IPs and DoH GET requests, which BlahDNS no longer accepts. For current servers see [server-conf/Readme.MD](../../server-conf/Readme.MD).

## DoH over HTTP/3 example (doh-jp)

Moved from `client-conf/DoT-or-DoH-Android.md`.

```
### Via `curl --http3` 
Mac OSX, installation guide: https://developers.cloudflare.com/http3/curl-brew
curl --http3 -H 'accept: application/dns-message' -v 'https://doh-jp.blahdns.com/dns-query?dns=q80BAAABAAAAAAAAA3d3dwdleGFtcGxlA2NvbQAAAQAB' | hexdump -C
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0*   Trying 139.162.112.47:443...
* Connect socket 5 over QUIC to 139.162.112.47:443
* Sent QUIC client Initial, ALPN: h3,h3-29,h3-28,h3-27
* Connected to doh-jp.blahdns.com () port 443 (#0)
* h3 [:method: GET]
* h3 [:path: /dns-query?dns=q80BAAABAAAAAAAAA3d3dwdleGFtcGxlA2NvbQAAAQAB]
* h3 [:scheme: https]
* h3 [:authority: doh-jp.blahdns.com]
* h3 [user-agent: curl/7.78.0-DEV]
* h3 [accept: application/dns-message]
* Using HTTP/3 Stream ID: 0 (easy handle 0x7f9e6e00c200)
> GET /dns-query?dns=q80BAAABAAAAAAAAA3d3dwdleGFtcGxlA2NvbQAAAQAB HTTP/3
> Host: doh-jp.blahdns.com
> user-agent: curl/7.78.0-DEV
> accept: application/dns-message
>
< HTTP/3 200
< content-type: application/dns-message
<
{ [75 bytes data]
100    75    0    75    0     0    326      0 --:--:-- --:--:-- --:--:--   331
* Connection #0 to host doh-jp.blahdns.com left intact
00000000  ab cd 81 a0 00 01 00 01  00 00 00 01 03 77 77 77  |.............www|
00000010  07 65 78 61 6d 70 6c 65  03 63 6f 6d 00 00 01 00  |.example.com....|
00000020  01 03 77 77 77 07 65 78  61 6d 70 6c 65 03 63 6f  |..www.example.co|
00000030  6d 00 00 01 00 01 00 00  34 a0 00 04 5d b8 d8 22  |m.......4...].."|
00000040  00 00 29 10 00 00 00 80  00 00 00                 |..)........|
0000004b

### Via Docker curl

docker run -it --rm ymuski/curl-http3 curl --http3 -H 'accept: application/dns-message' -v 'https://doh-jp.blahdns.com/dns-query?dns=q80BAAABAAAAAAAAA3d3dwdleGFtcGxlA2NvbQAAAQAB' | hexdump -C
```

## personalDNSfilter entries for retired servers and old Singapore IPs

Moved from `client-conf/DoT-or-DoH-Android.md`.

```
95.216.212.177::443::DOH::https://doh-fi.blahdns.com/dns-query
139.162.112.47::443::DOH::https://doh-jp.blahdns.com/dns-query
45.91.92.121::443::DOH::https://doh-ch.blahdns.com/dns-query
192.53.175.149::443::DOH::https://doh-sg.blahdns.com/dns-query
95.216.212.177::853::DOT::dot-fi.blahdns.com
139.162.112.47::853::DOT::dot-jp.blahdns.com
45.91.92.121::853::DOT::dot-ch.blahdns.com
192.53.175.149::853::DOT::dot-sg.blahdns.com
[2a01:4f9:c010:43ce::1]::853::DOT::dot-fi.blahdns.com
[2400:8902::f03c:92ff:fe27:344b]::853::DOT::dot-jp.blahdns.com
[2400:8901::f03c:92ff:fe27:870a]::853::DOT::dot-sg.blahdns.com
[2a0e:dc0:6:23::2]::853::DOT::dot-ch.blahdns.com
[2a01:4f9:c010:43ce::1]::443::DOH::https://doh-fi.blahdns.com/dns-query
[2400:8902::f03c:92ff:fe27:344b]::443::DOH::https://doh-jp.blahdns.com/dns-query
[2400:8901::f03c:92ff:fe27:870a]::443::DOH::https://doh-sg.blahdns.com/dns-query
[2a0e:dc0:6:23::2]::443::DOH::https://doh-ch.blahdns.com/dns-query
```

## Yggdrasil addresses of retired servers

Moved from `client-conf/yggdrasil.md`.

```
    forward-addr: 200:e338:984b:9635:503b:36ef:f56a:5b51@853#dot-fi.blahdns.com
    forward-addr: 201:b09c:4dc1:8d15:e34:3f68:679:73b8@853#dot-jp.blahdns.com
    forward-addr: 202:83df:29be:662e:c3f2:13df:813d:c3d1@853#dot-ch.blahdns.com
Japan: 201:b09c:4dc1:8d15:e34:3f68:679:73b8
Finland: 200:e338:984b:9635:503b:36ef:f56a:5b51
Switzerland: 202:83df:29be:662e:c3f2:13df:813d:c3d1
```

## stunnel example (Japan)

Moved from `client-conf/stunnel.md`.

```
// blahdns.conf
debug = err
[blahdns-dns]
client = yes
accept = 127.0.0.1:5353
connect = 139.162.112.47 #Japan

verifyChain = yes
CApath = /etc/ssl/certs

checkHost = dot-jp.blahdns.com
```

## AdGuard dnsproxy example (Japan)

Moved from `client-conf/dnsproxy/README.md`.

```
./dnsproxy -l ::1 -l 127.0.0.1 -p 53 -u quic://dot-jp.blahdns.com:784 -f 1.0.0.2:53 -b 1.0.0.2:53 --refuse-any
```

## dnsproxy.service ExecStart (Japan + Singapore)

Moved from `client-conf/dnsproxy/dnsproxy.service`.

```
ExecStart=/usr/local/bin/dnsproxy -l ::1 -l 127.0.0.1 -p 53 -u quic://dot-jp.blahdns.com:784 -u quic://dot-sg.blahdns.com:784 -f 1.0.0.2:53 -b 1.0.0.2:53 --refuse-any
```

## Unbound forward-addr lines (retired servers, old Singapore IPs)

Moved from `client-conf/unbound.conf`.

```
forward-addr: 95.216.212.177@443#dot-fi.blahdns.com
forward-addr: 2a01:4f9:c010:43ce::1@853#dot-fi.blahdns.com
forward-addr: 212.52.0.233@853#dot-jp.blahdns.com
forward-addr: 2406:ef80:4:1537::1@853#dot-jp.blahdns.com
forward-addr: 45.91.92.121@853#dot-ch.blahdns.com
forward-addr: 2a0e:dc0:6:23::2@853#dot-ch.blahdns.com
forward-addr: 103.167.150.45@853#dot-sg.blahdns.com
forward-addr: 2406:ef80:2:5ee4::1@853#dot-sg.blahdns.com
```

## DoH JSON GET example (doh-jp)

Moved from `client-conf/README.md`.

```
curl -H 'accept: application/dns-json' 'https://doh-jp.blahdns.com/dns-query?name=www.google.com&type=A'
```

## DNSCrypt v1 (retired)

Moved from `FAQ.md`.

```
## DnscryptV1 (updated 2019-10-02 GMT +8) 

dnscrypt-proxy --provider-key=5384:E814:4314:293E:56DD:1B14:0A1E:F172:AD47:BDBA:1799:C895:7294:953D:034E:B5C7
                 --resolver-address=108.61.201.119
                 --provider-name=2.dnscrypt-cert.blahdns.com
```

## Old troubleshooting commands (doh-jp, doh1, doh2, DoH GET, DoT on port 443)

Moved from `FAQ.md`.

```
## Troubleshoot 


// DNS dnsentropy check
dig +short porttest.dns-oarc.net TXT
Answer: porttest.y.x.w.v.u.t.s.r.q.p.o.n.m.l.k.j.i.h.g.f.e.d.c.b.a.pt.dns-oarc.net.
"159.69.198.101 is GREAT: 53 queries in 2.7 seconds from 53 ports with std dev 14045"

// Browser test: 
https://doh-de.blahdns.com/dns-query?name=example.net
https://doh-jp.blahdns.com/dns-query?name=example.net
https://doh2.blahdns.com/dns-query?ct=application/dns-json&name=google.de&type=A&edns_client_subnet=0.0.0.0/0
https://doh1.blahdns.com/dns-query?ct=application/dns-json&name=google.de&type=AAAA&edns_client_subnet=0.0.0.0/0

// curl with DoH 
curl -H 'content-type: application/dns-message' -vL -v 'https://doh-jp.blahdns.com/dns-query?dns=AAABAAABAAAAAAAAA3d3dwdleGFtcGxlA2NvbQAAAQAB' | hexdump -C

curl -H 'content-type: application/dns-message' -vL -v 'https://doh-de.blahdns.com/dns-query?dns=AAABAAABAAAAAAAAA3d3dwdleGFtcGxlA2NvbQAAAQAB' | hexdump -C

// Kdig on Ubuntu, Debian
apt install knot-dnsutils

// Kdig TLS with port 853, port 443 force include SNI (updated on August 1, 2019)

kdig @159.69.198.101 +tls example.com 
kdig @2a01:4f8:1c1c:6b4b::1 +tls example.com 

kdig @159.69.198.101 +tls -p 443 +tls-sni=dot-de.blahdns.com example.com 
kdig @2a01:4f8:1c1c:6b4b::1 +tls -p 443 +tls-sni=dot-de.blahdns.com example.com 

// TLS certificate validation 

kdig -d @159.69.198.101 -p 443 +tls-sni=dot-de.blahdns.com +tls-ca +tls-host=dot-de.blahdns.com example.com
kdig -d @2a0a:e5c0:2:2:0:c8ff:fe68:bf48 -p 443 +tls-sni=dot-de.blahdns.com +tls-ca +tls-host=dot-de.blahdns.com example.com
```

## macOS Mojave OpenSSL TLS 1.3 (doh-jp)

Moved from `FAQ.md`.

```
## Mac OSX Mojave use Openssl TLS 1.3 


brew upgrade
brew install openssl@1.1

// Put openssl tls 1.3 as first choice on zsh, paste it and restart terminal
echo 'export PATH="/usr/local/opt/openssl@1.1/bin:$PATH"' >> ~/.zshrc

// Debug DoH with TLS 1.3
openssl s_client -state -debug -msg -connect doh-jp.blahdns.com:443 -tls1_3
```
