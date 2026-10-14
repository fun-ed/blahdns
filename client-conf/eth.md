# Open `.eth` (ENS) sites with BlahDNS

BlahDNS resolves every `.eth` name to the BlahDNS ENS gateway. The gateway reads the name's ENS content hash from Ethereum and serves the site from IPFS. You only need to use BlahDNS as your resolver and open the site with **plain HTTP**:

```
http://vitalik.eth/
http://matoken.eth/
```

## Limits

* **HTTP only.** No public CA issues certificates for `.eth`, so `https://<name>.eth` is refused on purpose (the TLS handshake is rejected). There is no HTTPS mirror such as `<name>.eth.blahdns.com`.
* Only `A` and `AAAA` records are answered for `.eth`; other types (TXT, dnslink, ...) return no data.
* A name without an ENS content hash returns `404 Requested ENS name does not have a content hash set.`
* Only `GET` and `HEAD` requests. Per-client rate limits apply (HTTP 429 when exceeded). Names reported for abuse may be blocked (HTTP 451).
* The gateway keeps no access logs.

## 1. Use BlahDNS as your resolver

Any BlahDNS endpoint works (DoT, DoH, DoQ, DTLS, DNSCrypt); see the [server list](../server-conf/Readme.MD) and the [client examples](README.md). Examples:

* Android "Private DNS": `dot-sg.blahdns.com` or `dot-de.blahdns.com`.
* Firefox: Settings → Privacy & Security → DNS over HTTPS → Max protection → custom provider `https://doh-sg.blahdns.com/dns-query`.
* Chrome / Edge: Settings → Privacy → Use secure DNS → custom `https://doh-de.blahdns.com/dns-query`. If the browser's secure DNS points to another provider, it will not see `.eth` names.

## 2. Allow plain HTTP for `.eth`

Browsers that upgrade every page to HTTPS will show a warning or fail, because `https://<name>.eth` is refused:

* Firefox HTTPS-Only Mode: on the warning page choose "Continue to HTTP Site", or add an exception for the site.
* Chrome "Always use secure connections": choose "Continue to site" on the warning page.
* Brave handles ENS by itself when its Web3 ENS setting is enabled; in that case it does not ask BlahDNS.

Type the full address with `http://`; without it some browsers treat `name.eth` as a search term.

## 3. Check

```sh
# The name resolves through BlahDNS (DNS-over-TLS)
kdig +short @dot-sg.blahdns.com +tls-ca +tls-host=dot-sg.blahdns.com vitalik.eth A
# The gateway answers
curl -sI http://vitalik.eth/ | head -1     # HTTP/1.1 200 OK (curl must use BlahDNS as the system resolver)
```

If `kdig` prints an address but the browser does not open the site, the browser is not using BlahDNS (step 1) or is forcing HTTPS (step 2).
