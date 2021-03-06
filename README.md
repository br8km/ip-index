# IP Index
A fast offline IP lookup library. Returns blacklist status, detects VPN/hosting and shows geo info.

## How are/were the datacenter ranges detected

* [This list](https://udger.com/resources/datacenter-list) of Datacenters was manually converted to a list of ASNs.
* The ASNs from [these](https://github.com/linuxclark/web-hosting-companies) [lists](https://github.com/brianhama/bad-asn-list) were added.
* List of all ASNs names is [matched](src/matches.js) against keywords that would give away datacenters or hosting

False positives are possible.

## Sanity check

Pick some random IPs:

```shell script
sort -R dist/datacenters.netset | head -n 5
```

Check against any of the known IP scoring services:
* https://www.ipqualityscore.com/free-ip-lookup-proxy-vpn-test/lookup/1.1.1.1
* https://www.ip2location.com/demo/1.1.1.1
* https://scamalytics.com/ip/1.1.1.1

## Usage

Install dependencies and generate a DB
```shell script
npm run deps:install
TOKEN={IP2LOCATION_DOWNLOAD_TOKEN} npm run db:build
```

Run the [example file](src/example.js):

```shell script
node ./src/example.js`
```

Output:
```
init: 1.074ms
Datacenter: false
Blacklisted: true
Country: de
Asn: { id: 3320, name: 'Deutsche Telekom AG' }
queries: 3.759ms
```

## Used projects

* [Firehol](https://github.com/firehol/blocklist-ipsets)
* [ip2location ASN DB](https://lite.ip2location.com/database/ip-asn)
* [This list of DC names](https://udger.com/resources/datacenter-list)
* [This list of ASNs](https://github.com/brianhama/bad-asn-list)
* [This list of web-hosting companies](https://github.com/linuxclark/web-hosting-companies)

## Acknowledgments
* This product includes IP2Location LITE data available from [http://www.ip2location.com](http://www.ip2location.com).
* This product includes GeoLite2 data created by MaxMind, available from [https://www.maxmind.com](https://www.maxmind.com).
