```
man tcpdump | less //show help with commands!!
```

``sudo tcpdump -i wlan0 -n host example.com``

//capture only trafic from https:{}//example.com

``sudo tcpdump -i wlan0 -n src example.com``
//capture only packets from the src 10.0.2.15
![[Pasted image 20250125131211.png]]

``sudo tcpdump -i wlan0 -n dst example.com``
//destination
![[Pasted image 20250125131244.png]]

``sudo tcpdump -i wlan0 -n net example.com``
//capture to and from specific network
![[Pasted image 20250125131419.png]]

``sudo tcpdump -i wlan0 -n port 4432
//capture traffic from specific port. Also possible to use `src port` and `dst port`:
![[Pasted image 20250125131534.png]]

**Save to a file**

``sudo tcpdump -i wlan0 -n -w ~/Desktop/capture.pcap``

## Logical Operators (and, or, not)

![[Pasted image 20250125131702.png]]
![[Pasted image 20250125131736.png]]
![[Pasted image 20250125131836.png]]

## Another

``tcpdump -r 2024-04-18.pcap --count``

``tcpdump -tt -r 2024-04-18.pcap -n tcp | cut -d " " -f 3 | cut -d "." -f 1-4`` //cut only IP's without ports and date and another...

``tcpdump -tt -r 2024-04-18.pcap -n tcp | cut -d " " -f 3 | cut -d "." -f 1-4 | sort | uniq -c | sort -nr`` //show also count and uniq IPs only

--------
![[Pasted image 20250126153729.png]]

## Quest

![[Pasted image 20250126160911.png]]
```
tcpdump -r tcpdump_challenge.pcap --count
tcpdump -r tcpdump_challenge.pcap -n icmp --count
tcpdump -nn -r tcpdump_challenge.pcap icmp //find dst 172.67.72.15
whois 172.67.72.15 | grep -i "origin\|asn"
```
![[Pasted image 20250126163353.png]]
```
tcpdump -nn -r tcpdump_challenge.pcap -A | grep -i "POST " | wc -l
----
tcpdump -nn -r tcpdump_challenge.pcap -A | grep -i "POST"
tcpdump -nn -r tcpdump_challenge.pcap -A | grep -i "password"
----
tcpdump -nn -r tcpdump_challenge.pcap 'tcp' | awk '{print $5}' | cut -d'.' -f2 | sort | uniq -c | sort -nr //change '{print ${/_5_/}}'
```
![[Pasted image 20250126164449.png]]
```
tcpdump -nn -r tcpdump_challenge.pcap -A 'tcp port 21' | grep -i "USER\|PASS" | grep -vi "User-Agent" //exclude User-Agent here
---
tcpdump -nn -r tcpdump_challenge.pcap -A 'tcp port 21' | grep -i "RETR"
---
tcpdump -nn -r tcpdump_challenge.pcap -A 'tcp port 80' | grep -i "User-Agent" //then find User-Agent: TeslaBrowser/5.5 - its malware
```
![[Pasted image 20250126165016.png]]
```
tcpdump -nn -r tcpdump_challenge.pcap -A | grep -i "User-Agent: TeslaBrowser/5.5" -A 20
---
tcpdump -nn -r tcpdump_challenge.pcap -A | grep -i "Location: https://www.youtube.com"
```