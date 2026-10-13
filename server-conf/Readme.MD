## Configuration details 

```
# DNSCrypt information
# Singapore
Provider public key: 7b8bf43c61a5207cecf803627e2497d327557585837a85b87e8700e8d989ad87
Provider name: 2.dnscrypt-cert.blahdns.com
# Germany
Provider public key: 3395cf21200ed866f8ab3fec7c949f4a374510708f2fa90258d9c1d53ffd14db
Provider name: 2.dnscrypt-cert.blahdns.com
```

DNS-over-HTTPS accepts POST requests only (RFC 8484 wire format); GET returns 403. DNS-over-TLS is served on port 853. DNS-over-QUIC is served on the `dot-*` hostnames.

- Germany (DoT, DoH, Dnscryptv2, DoQ, DoH-http3), Provider: Hetzner
  * IP: 78.46.244.143, 2a01:4f8:c17:ec67::1
  * DNS-over-HTTPS: 
    * https://doh-de.blahdns.com/dns-query
    * h3://doh-de.blahdns.com/dns-query
  * DNS-over-QUIC:
    * quic://dot-de.blahdns.com:784
  * DNS-over-TLS: 
    * tls://dot-de.blahdns.com:853
  * DNSCrypt:
    * ipv4: sdns://AQMAAAAAAAAAEjc4LjQ2LjI0NC4xNDM6ODQ0MyAzlc8hIA7YZvirP-x8lJ9KN0UQcI8vqQJY2cHVP_0U2xsyLmRuc2NyeXB0LWNlcnQuYmxhaGRucy5jb20
    * ipv6: sdns://AQMAAAAAAAAAG1syYTAxOjRmODpjMTc6ZWM2Nzo6MV06ODQ0MyAzlc8hIA7YZvirP-x8lJ9KN0UQcI8vqQJY2cHVP_0U2xsyLmRuc2NyeXB0LWNlcnQuYmxhaGRucy5jb20

- Singapore (DoT, DoH, Dnscryptv2, DoQ, DoH-http3), Provider: Contabo
  * IP: 46.250.226.242, 2407:3640:2205:1668::1
  * DNS-over-HTTPS: 
    * https://doh-sg.blahdns.com/dns-query
    * h3://doh-sg.blahdns.com/dns-query
  * DNS-over-QUIC:
    * quic://dot-sg.blahdns.com:784
  * DNS-over-TLS: 
    * tls://dot-sg.blahdns.com:853
  * DNSCrypt:
    * ipv4: sdns://AQMAAAAAAAAAEzQ2LjI1MC4yMjYuMjQyOjg0NDMge4v0PGGlIHzs-ANifiSX0ydVdYWDeoW4focA6NmJrYcbMi5kbnNjcnlwdC1jZXJ0LmJsYWhkbnMuY29t
    * ipv6: sdns://AQMAAAAAAAAAHVsyNDA3OjM2NDA6MjIwNToxNjY4OjoxXTo4NDQzIHuL9DxhpSB87PgDYn4kl9MnVXWFg3qFuH6HAOjZia2HGzIuZG5zY3J5cHQtY2VydC5ibGFoZG5zLmNvbQ
