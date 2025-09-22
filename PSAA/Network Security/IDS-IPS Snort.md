![[Pasted image 20250126182647.png]]

## IPS

`sudo snort -i wlan0`
`sudo snort -i wlan0 -d` //ACII format
`sudo snort -i wlan0 -d -l /var/log/snort`  //download output to logs
`sudo tcpdump -r snort.log.132352353`

---------

## IDS 

To create AUTOMATIC rules go to **SNORTY**
- [http://snorpy.cyb3rs3c.net/](http://snorpy.cyb3rs3c.net/) (Alternative URL: [https://anir0y.in/snort2-rulgen/](https://anir0y.in/snort2-rulgen))

![[Pasted image 20250126190656.png]]

**Брутфорс Атака!!** Якщо більше 5 спроб входу за 30 секунд, то згенерувати "алерт":
![[Pasted image 20250126191650.png]]

# PRACTICE HERE (pcap to test):

- [https://www.malware-traffic-analysis.net/](https://www.malware-traffic-analysis.net/)
- [https://chrissanders.org/packet-captures/](https://chrissanders.org/packet-captures/)
- [https://github.com/chrissanders/packets](https://github.com/chrissanders/packets)
- [https://wiki.wireshark.org/SampleCaptures](https://wiki.wireshark.org/SampleCaptures)
- [https://www.netresec.com/?page=PcapFiles](https://www.netresec.com/?page=PcapFiles)
- [https://github.com/zeek/zeek/tree/master/testing/btest/Traces](https://github.com/zeek/zeek/tree/master/testing/btest/Traces)
- ﻿[https://docs.securityonion.net/en/2.4/pcaps.html](https://docs.securityonion.net/en/2.4/pcaps.html)