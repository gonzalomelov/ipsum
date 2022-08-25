![Logo](https://i.imgur.com/PyKLAe7.png)

[![License](https://img.shields.io/badge/license-The_Unlicense-red.svg)](https://unlicense.org/)

About
----

**IPsum** is a threat intelligence feed based on 30+ different publicly available [lists](https://github.com/stamparm/maltrail) of suspicious and/or malicious IP addresses. All lists are automatically retrieved and parsed on a daily (24h) basis and the final result is pushed to this repository. List is made of IP addresses together with a total number of (black)list occurrence (for each). Greater the number, lesser the chance of false positive detection and/or dropping in (inbound) monitored traffic. Also, list is sorted from most (problematic) to least occurent IP addresses.

As an example, to get a fresh and ready-to-deploy auto-ban list of "bad IPs" that appear on at least 3 (black)lists you can run:

```
curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1
```

If you want to try it with `ipset`, you can do the following:

```
sudo su
apt-get -qq install iptables ipset
ipset -q flush ipsum
ipset -q create ipsum hash:net
for ip in $(curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1); do ipset add ipsum $ip; done
iptables -D INPUT -m set --match-set ipsum src -j DROP 2>/dev/null
iptables -I INPUT -m set --match-set ipsum src -j DROP
```

In directory [levels](levels) you can find preprocessed raw IP lists based on number of blacklist occurrences (e.g. [levels/3.txt](levels/3.txt) holds IP addresses that can be found on 3 or more blacklists).

Wall of Shame (2022-08-25)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
144.172.73.16|tor-exit4.riverside.rocks|9
89.234.157.254|marylou.nos-oignons.net|8
95.214.24.192|-|8
171.25.193.78|tor-exit-read-me.dfri.se|8
144.172.73.66|tor-exit3.riverside.rocks|8
179.60.147.161|-|8
103.251.167.21|tor-exit-at-the.quesadilla.party|8
64.113.32.29|tor.t-3.net|8
80.82.77.33|sky.census.shodan.io|7
162.247.74.202|-|7
171.25.193.77|tor-exit-read-me.dfri.se|7
185.220.100.255|tor-exit-4.zbau.f3netze.de|7
185.220.100.254|tor-exit-3.zbau.f3netze.de|7
165.227.211.85|-|7
162.241.70.133|162-241-70-133.webhostbox.net|7
192.42.116.16|tor-exit.hartvoorinternetvrijheid.nl|7
171.251.31.142|dynamic-adsl.viettel.vn|7
159.89.44.77|-|7
199.195.254.191|2.tor-exit.neelc.org|7
80.67.172.162|algrothendieck.nos-oignons.net|7
45.139.122.241|-|7
185.129.62.62|tor01.zencurity.com|7
158.69.63.54|torex2.fissionrelays.net|7
