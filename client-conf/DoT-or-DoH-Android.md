## DoH over HTTP/3, UDP (protocol QUIC)

BlahDNS DoH accepts POST requests only (RFC 8484 wire format); GET requests return 403.

### Via `curl --http3`
Mac OSX, installation guide: https://developers.cloudflare.com/http3/curl-brew
```
printf 'AAABAAABAAAAAAAAA3d3dwdleGFtcGxlA2NvbQAAAQAB' | base64 -d | curl -s --http3 -H 'content-type: application/dns-message' --data-binary @- https://doh-sg.blahdns.com/dns-query | hexdump -C
```

### Via Docker curl

```
printf 'AAABAAABAAAAAAAAA3d3dwdleGFtcGxlA2NvbQAAAQAB' | base64 -d | docker run -i --rm ymuski/curl-http3 curl -s --http3 -H 'content-type: application/dns-message' --data-binary @- https://doh-sg.blahdns.com/dns-query | hexdump -C
```

## DoT and DoH on Android

### Solution 1 with Nebulo app

1. Use app [Nebulo](https://play.google.com/store/apps/details?id=com.frostnerd.smokescreen)
2. Follow tutorial down below to setup blahdns
  1. Manually type the server settings shown below

**DoH**


<img src="https://github.com/fun-ed/blahdns/raw/master/client-conf/img-source/nebulo-doh.jpg" alt="Your image title" width="250"/>


**DoT**


<img src="https://github.com/fun-ed/blahdns/raw/master/client-conf/img-source/nebulo-dot.jpg" alt="Your image title" width="250"/>


### Solution 2 with personalDNSfilter app (Android)

App download: [https://zenz-solutions.de/personaldnsfilter](https://zenz-solutions.de/personaldnsfilter)


**Config file**

```
## DoH with adblock (Germany, Singapore)

78.46.244.143::443::DOH::https://doh-de.blahdns.com/dns-query
46.250.226.242::443::DOH::https://doh-sg.blahdns.com/dns-query

## DoT 
78.46.244.143::853::DOT::dot-de.blahdns.com
46.250.226.242::853::DOT::dot-sg.blahdns.com

## Ipv6 DoT
[2a01:4f8:c17:ec67::1]::853::DOT::dot-de.blahdns.com
[2407:3640:2205:1668::1]::f03c:92ff:fe27:870a]::853::DOT::dot-sg.blahdns.com

## Ipv6 DoH
[2a01:4f8:c17:ec67::1]::443::DOH::https://doh-de.blahdns.com/dns-query
[2407:3640:2205:1668::1]::f03c:92ff:fe27:870a]::443::DOH::https://doh-sg.blahdns.com/dns-query
```


<img src="https://github.com/fun-ed/blahdns/raw/master/client-conf/img-source/personal-dnsfilter-1.jpg" alt="Your image title" width="250"/>
<img src="https://github.com/fun-ed/blahdns/raw/master/client-conf/img-source/personal-dns-filter2.jpg" alt="Your image title" width="250"/>


### Solution 3 Android Pie 

For Android 9 Pie user, Go to Setting -> Wi-Fi -> Private DNS, and enter `dot-sg.blahdns.com` or `dot-de.blahdns.com` 

