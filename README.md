# NETWORKING

## CODE

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


## ip addr show eth0
```
10: eth0@if11: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
    link/ether 02:42:ac:11:00:04 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 172.17.0.4/16 brd 172.17.255.255 scope global eth0
       valid_lft forever preferred_lft forever
```
       
       
## ip route show
```
default via 172.17.0.1 dev eth0
172.17.0.0/16 dev eth0 proto kernel scope link src 172.17.0.4
172.18.0.0/16 dev docker0 proto kernel scope link src 172.18.0.1 linkdown
```


## ping -c3 8.8.8.8
```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=114 time=2.55 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=114 time=0.764 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=114 time=1.07 ms

--- 8.8.8.8 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2047ms
rtt min/avg/max/mdev = 0.764/1.459/2.545/0.777 ms
```

- computer has internet access
- computer at 8.8.8.8 is up and running
- there is a web site at http://8.8.8.8
- isp knows how to send traffic towards google


## host -t aaaa google.com
```
google.com has IPv6 address 2a00:1450:4013:c1a::64
google.com has IPv6 address 2a00:1450:4013:c1a::65
google.com has IPv6 address 2a00:1450:4013:c1a::66
google.com has IPv6 address 2a00:1450:4013:c1a::8b
```



## host -t mx udacity.com
```
udacity.com mail is handled by 10 aspmx.l.google.com.
udacity.com mail is handled by 20 alt1.aspmx.l.google.com.
udacity.com mail is handled by 20 alt2.aspmx.l.google.com.
udacity.com mail is handled by 30 alt3.aspmx.l.google.com.
udacity.com mail is handled by 30 alt4.aspmx.l.google.com.
```

## tcpdump -n -c5 -i eth0 port22
```
tcpdump: eth0: You don't have permission to capture on that device
(socket: Operation not permitted)
```

## traceroute www.udacity.com
```
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
```

## printf 'HEAD / HTTP/1.1\r\nHost: www.udacity.com\r\n\r\n' | nc www.udacity.com 80
```
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
```

ssh server port 22
http server port 80


## printf 'HEAD / HTTP/1.1\r\nHost: en.wikipedia.org\r\n\r\n' | nc en.wikipedia.org 80
```
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
```

output of printf used as an input to nc through pipe, nc takes that input and sends it to the port that it is told and displays the outcome.

nc -n [IP address] port (-n only number or ip address)
nc -v example.com 80


## printf 'HEAD / HTTP/1.1\r\nHost: www.google.com\r\n\r\n' | nc www.google.com 80
```
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
```

## Google uses server gws


- layer-application  --  protocols-http, ssh  --  concepts-URLs, password, webpages, server headers
- layer-transport  --  protocols-tcp, udp  --  concepts-port numbers, sessions
- layer-internet  --  protocols-IP  --  concepts-IP addresses, routes
- layer-hardware  --  protocols-wifi, ethernet, DSL  --  concepts-signal strength, access points

## communication between terminals
I opened two different terminals, into the first one I wrote
```
nc -l 3456
```
and into the second one I wrote:
```
nc localhost 3456
```

this allowed me to write messages between two terminals, the first terminal was listening to the second one.
CTRL+C ended the listening.


## port numbers
highest port number 65 535
lowest port number 1023
0-1023 reserved for superuser

## sudo lsof -i
```
COMMAND     PID             USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
sshd         71             root    3u  IPv4  34960      0t0  TCP *:ssh (LISTEN)
sshd         71             root    4u  IPv6  34962      0t0  TCP *:ssh (LISTEN)
theia-pro   330             root    6u  IPv6  34548      0t0  TCP *:970 (LISTEN)

```

## 
```
ping -c 7 yahoo.com
-c 7 will send 7 pings and then exit

host -t a voog.com shows google's ip address
dig www.voog.com shows pretty much same info but in a form readable for scripts and closer to a way it's stored in a DNS server's configuration files.

```

```
CNAME - canonical name
AAAA - IPv6 address
NS - DNS name server

```

```
IPv4 
216.58.203.121
0-255, each is one byte-8bits
```

```
how many ipv4 addresses are there?
over 4 billion

```

/24 netblock:
225.225.225.0

/16 netblock
225.225.0.0

decimal subnet mask /14 like stanford
255.252.0.0
around 250 000 addresses on that network


ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether 02:42:f0:ed:37:80 brd ff:ff:ff:ff:ff:ff
    inet 172.18.0.1/16 brd 172.18.255.255 scope global docker0
       valid_lft forever preferred_lft forever
10: eth0@if11: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
    link/ether 02:42:ac:11:00:04 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 172.17.0.4/16 brd 172.17.255.255 scope global eth0
       valid_lft forever preferred_lft forever

loopback almost always 127.0.0.1 allows programs to use the network stack to talk to other programs on the same host

ip route show default
default via 172.17.0.1 dev eth0
ping time less than 0.1 ms

* my public ipv4 82.131.29.235

* my private ipv found under system prefrences - network

```
ipv4 - 32 bit address length
ipv6 - 128 bit address length

```

- ipv4 does not produce enought addresses for the worlds population
- ipv6 is the next generation
- (ipv5 was a failed experiment)

* none of my devices have ipv6

```
What is a flag?
In low-level computer languages, a flag is a Boolean value — a true or false value — that is stored in memory as a single bit. If a flag bit is 1, we say the flag is set. If the flag bit is 0, the flag is cleared (or unset).
```

* SYN (synchronize) [S] — This packet is opening a new TCP session and contains a new initial sequence number.
* FIN (finish) [F] — This packet is used to close a TCP session normally. The sender is saying that they are finished sending, but they can still receive   data from the other endpoint.
* PSH (push) [P] — This packet is the end of a chunk of application data, such as an HTTP request.
* RST (reset) [R] — This packet is a TCP error message; the sender has a problem and wants to reset (abandon) the session.
* ACK (acknowledge) [.] — This packet acknowledges that its sender has received data from the other endpoint. Almost every packet except the first SYN       will have the ACK flag set.
* URG (urgent) [U] — This packet contains data that needs to be delivered to the application out-of-order. Not used in HTTP or most other current           applications.

```
tcp congestion control, so everything doesn't jam up.
(Screenshot-tcpcongestion)
````


```
traceroute + adress to see the route it took
or "mtr"

´´´

high latency - laggy

```
bandwitdh and latency - added pictures
´´´

besides retransmitting dropped packets, what does tcp need to do to make sure everyone gets to talk to the moon without too much congestion?
- when packets are dropped, send more slowly.

```
Firewalls are devices that network operators can use to filter traffic that's coming into or leaving their network. A firewall is one example of a class of network devices called middleboxes — devices that inspect, modify, or filter network traffic. Other examples of middleboxes include intrusion detection systems and load balancers. Technically, it's only a middle-box if it's a separate device from the client or server — server-side "firewalls" like Linux iptables aren't middleboxes.

´´´

A firewall can be a real boon to an organization's network security. The most common configuration for a firewall is to drop any incoming traffic except traffic to (host, port) pairs that are supposed to be receiving connections from the Internet. This lets the network administrator be sure that other machines on the network — like backend databases or administrative systems — aren’t going to get direct attacks from outside.

But firewalls can cause trouble for application developers. If you're trying to test or deploy a network app and there's a firewall between your server and the user, that firewall can potentially interfere with your app or block it completely. In order to deploy an application on a particular server and port, it helps to know what kind of firewall might be between you and your user. One of the reasons that many non-Web applications use HTTP as a transport is that HTTP is often unblocked at firewalls even when other ports are blocked.

Aside from blocking traffic outright, middleboxes can also alter traffic, for instance replacing web pages with error messages. This is often done for social or political purposes. For instance, in the U.S., many schools use traffic filters of various sorts to prevent students from accessing web sites deemed inappropriate for children. But what sites get counted as "inappropriate" can reflect the biases or opinions of the people who wrote or configured the filter.

And people who program these things can always make mistakes, too. For instance, there's a whole class of bugs that arise from filters that try to block rude words, but end up blocking or replacing innocuous words that contain a rude word as a substring.

Rather famously, some countries have deployed large-scale firewalls or filters to censor their citizens' access to the global Internet. Major well-known sites such as YouTube and Twitter are sometimes blocked entirely in some countries. That can happen to your site, too — just something to keep in mind.

```
some users cant access site, what should you investigate?
* can the user ping your site by IP address
* can the user access different domain on the same server
* can they look up your servers name using "host" or "dig"
* are all the users with the same problem in the same country

´´´

------------------------------
```
Middleboxes 2: Proxies & NAT
´´´
Earlier in this course, you learned about the IPv4 address shortage; and the deployment of Network Address Translation, or NAT, as a workaround for it. With NAT, several devices can access Internet resources through a single public IP address, with the NAT device using port numbers to match up connections on the inside and outside.

For end-users, NAT devices overlap with firewalls. Typical home routers can act as both a NAT and a simple firewall, often having the ability to block or filter at a very basic level. At a larger scale, ISPs and other organizations have deployed NAT devices for their whole customer networks, called carrier-grade NAT. This is very common for mobile networks, and also for ISPs in the developing world, where there never were anywhere near enough addresses allocated for the number of users.

Usually we imagine an end-user computer as having only one person using it at a time. After all, there's generally only one mouse and keyboard. Two people typing on the same keyboard at the same time doesn't generally happen outside of poorly thought-out TV shows. But in the case of NAT, your web site can see requests from the same IP address that actually come from different users on different computers.

Another way that can happen is through the use of web proxies. Whereas a NAT works at the IP level, rewriting packets, a web proxy works at the HTTP level, taking queries from browsers and sending them out to web servers. Many organizations use web proxies for caching, including some ISPs. From the standpoint of a web developer or site operator, traffic from a busy proxy looks much the same as traffic from a busy NAT: queries for many users, on many actual computers, are funneled through a single public IP address.

```
how could a web app distinguish users who are behind the same public IP address? - logged-in usewr identity and session cookies.







