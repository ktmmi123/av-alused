# Suur pealkiri

## alampealkiri1
teema üks
## alampealkiri2
teema kaks
## alampealkiri3
teema kolm

loetelu
- element1
- element2
  - element2.1

## kood

sudo apt-get update # uuendab paketinimekirjad
sudo apt-get upgrade # 

control + z - pausile
fg - toob tagasi esiplaanile
bg - viib taustale
kill %% 
control + c - katkestab 

ssh võtmed ja nende kasutamine 
- Webhosting 
- Github 


ip addr show eth0
```
10: eth0@if11: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
    link/ether 02:42:ac:11:00:04 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 172.17.0.4/16 brd 172.17.255.255 scope global eth0
       valid_lft forever preferred_lft forever
```
       
       
 ip route show
default via 172.17.0.1 dev eth0
172.17.0.0/16 dev eth0 proto kernel scope link src 172.17.0.4
172.18.0.0/16 dev docker0 proto kernel scope link src 172.18.0.1 linkdown



ping -c3 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=114 time=2.55 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=114 time=0.764 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=114 time=1.07 ms

computer has internet access
computer at 8.8.8.8 is up and running
there is a web site at http://8.8.8.8
isp knows how to send traffic towards google


--- 8.8.8.8 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2047ms
rtt min/avg/max/mdev = 0.764/1.459/2.545/0.777 ms



host -t aaaa google.com
google.com has IPv6 address 2a00:1450:4013:c1a::64
google.com has IPv6 address 2a00:1450:4013:c1a::65
google.com has IPv6 address 2a00:1450:4013:c1a::66
google.com has IPv6 address 2a00:1450:4013:c1a::8b




host -t mx udacity.com
udacity.com mail is handled by 10 aspmx.l.google.com.
udacity.com mail is handled by 20 alt1.aspmx.l.google.com.
udacity.com mail is handled by 20 alt2.aspmx.l.google.com.
udacity.com mail is handled by 30 alt3.aspmx.l.google.com.
udacity.com mail is handled by 30 alt4.aspmx.l.google.com.


tcpdump -n -c5 -i eth0 port22
tcpdump: eth0: You don't have permission to capture on that device
(socket: Operation not permitted)


traceroute www.udacity.com
traceroute to www.udacity.com (104.18.41.189), 30 hops max, 60 byte packets
 1  172.17.0.1 (172.17.0.1)  0.034 ms  0.009 ms  0.007 ms
 2  * * *
 3  * 104.18.41.189 (104.18.41.189)  6.182 ms 172.17.0.1 (172.17.0.1)  0.013 ms
 

My traceroute  [v0.94]
cs-34818560608-default (172.17.0.4) -> www.udacity.com                                                                                                                             2022-10-26T10:58:27+0000
Keys:  Help   Display mode   Restart statistics   Order of fields   quit
                                                                                                                                                                   Packets               Pings
 Host                                                                                                                                                            Loss%   Snt   Last   Avg  Best  Wrst StDev
 1. 172.17.0.1                                                                                                                                                    0.0%    44    0.1   0.1   0.1   0.1   0.0
 2. (waiting for reply)
 3. 172.64.146.67                                                                                                                                                 0.0%    43    4.6   4.7   4.3   6.0   0.3


printf 'HEAD / HTTP/1.1\r\nHost: www.udacity.com\r\n\r\n' | nc www.udacity.com 80
HTTP/1.1 301 Moved Permanently
Date: Wed, 26 Oct 2022 10:59:03 GMT
Connection: keep-alive
Cache-Control: max-age=3600
Expires: Wed, 26 Oct 2022 11:59:03 GMT
Location: https://www.udacity.com/
Set-Cookie: __cf_bm=m3Xgt3dXf1fCT_WRtmALqiLhJhTThiVB.z7jkpQF4gA-1666781943-0-AU5yb97KWiqeG4F8xoTB8VOqF7LEvL67GgzL7zFvNDrBmtwcxMxsjkfJ7tH2hQ5lKH2W+ZYfbxiTpKc6By5IoVCK3AdK1jpv/QxrKO710C/S; path=/; expires=Wed, 26-Oct-22 11:29:03 GMT; domain=.udacity.com; HttpOnly
X-Content-Type-Options: nosniff
Server: cloudflare
CF-RAY: 7602ae2dbbe5b837-AMS
alt-svc: h3=":443"; ma=86400, h3-29=":443"; ma=86400


ssh server port 22
http server port 80


printf 'HEAD / HTTP/1.1\r\nHost: en.wikipedia.org\r\n\r\n' | nc en.wikipedia.org 80

HTTP/1.1 301 TLS Redirect
Date: Wed, 26 Oct 2022 11:18:20 GMT
Server: Varnish
X-Varnish: 768499768
X-Cache: cp3050 int
X-Cache-Status: int-front
Server-Timing: cache;desc="int-front", host;desc="cp3050"
Permissions-Policy: interest-cohort=()
Set-Cookie: WMF-Last-Access=26-Oct-2022;Path=/;HttpOnly;secure;Expires=Sun, 27 Nov 2022 00:00:00 GMT
Set-Cookie: WMF-Last-Access-Global=26-Oct-2022;Path=/;Domain=.wikipedia.org;HttpOnly;secure;Expires=Sun, 27 Nov 2022 00:00:00 GMT
X-Analytics: public_cloud=1
X-Client-IP: 34.147.86.14
Location: https://en.wikipedia.org/
Content-Length: 0
Connection: keep-alive


output of printf used as an input to nc through pipe, nc takes that input and sends it to the port that it is told and displays the outcome.

nc -n [IP address] port (-n only number or ip address)
nc -v example.com 80


printf 'HEAD / HTTP/1.1\r\nHost: www.google.com\r\n\r\n' | nc www.google.com 80
HTTP/1.1 200 OK
Content-Type: text/html; charset=ISO-8859-1
Date: Wed, 26 Oct 2022 12:20:47 GMT
Server: gws
X-XSS-Protection: 0
X-Frame-Options: SAMEORIGIN
Transfer-Encoding: chunked
Expires: Wed, 26 Oct 2022 12:20:47 GMT
Cache-Control: private
Set-Cookie: AEC=AakniGOc2-6__NQYKVtz_lTCvM2GlfE8OLCn3kR0lSz_Zl7BrfVugYj_e-A; expires=Mon, 24-Apr-2023 12:20:47 GMT; path=/; domain=.google.com; Secure; HttpOnly; SameSite=lax

Google uses server gws


layer-application  --  protocols-http, ssh  --  concepts-URLs, password, webpages, server headers
layer-transport  --  protocols-tcp, udp  --  concepts-port numbers, sessions
layer-internet  --  protocols-IP  --  concepts-IP addresses, routes
layer-hardware  --  protocols-wifi, ethernet, DSL  --  concepts-signal strength, access points

I opened two different terminals, into the first one I wrote nc -l 3456
and into the second one I wrote:
nc localhost 3456

this allowed me to write messages between two terminals, the first terminal was listening to the second one.
CTRL+C ended the listening.

highest port number 65 535
lowest port number 1023
0-1023 reserved for superuser


sudo apt-get update
sudo apt-get install netcat-openbsd tcpdump traceroute mtr iputils-ping lsof


printf 'HEAD / HTTP/1.1\r\nHost: mail.tptlive.ee\r\n\r\n\r\n' | nc mail.tptlive.ee 80
HTTP/1.1 301 Moved Permanently
Date: Thu, 20 Oct 2022 12:00:39 GMT
Server: Apache/2.4.38 (Debian)
Location: https://mail.tptlive.ee/
Cache-Control: max-age=0
Expires: Thu, 20 Oct 2022 12:00:39 GMT
Content-Type: text/html; charset=iso-8859-1
Vary: Accept-Encoding
X-Varnish: 548897561
Age: 0
Via: 1.1 varnish (Varnish/5.2)
X-Cache: MISS
Connection: keep-alive


PKI   X.509
