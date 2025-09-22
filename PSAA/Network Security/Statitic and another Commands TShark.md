## Statistics | IPv4 and IPv6

tshark -r demo.pcapng -z ptype,tree -q
```
-z ptype,tree -q
```
You can filter all IP addresses using the parameters:
```
-z ip_hosts,tree -q
-z ipv6_hosts,tree -q
```

You can filter all source and destination addresses using
```
-z ip_srcdst,tree -q
-z ipv6_srcdst,tree -q
```
You can filter all outgoing traffic by using the parameters:
```
IPv4: -z dests,tree -q
IPv6: -z ipv6_dests,tree -q
```

## Statistics | DNS

Provides statistics on DNS packets by summarising the available info:

``-z dns,tree -q``

## Statistics | HTTP

- **Packet and status counter for HTTP:** `-z http,tree -q`
- **Packet and status counter for HTTP2:** `-z http2,tree -q`
- **Load distribution:** `-z http_srv,tree -q`
- **Requests:** `-z http_req,tree -q`
- **Requests and responses:** `-z http_seq,tree -q`

## Follow Stream

| **Main Parameter** | **Protocol**                        | **View Mode**    | **Stream Number**    | **Additional Parameter** |
| ------------------ | ----------------------------------- | ---------------- | -------------------- | ------------------------ |
| -z follow          | - TCP<br>- UDP<br>- HTTP<br>- HTTP2 | - HEX<br>- ASCII | 0 \| 1 \| 2 \| 3 ... | -q                       |
- **TCP Streams:** `-z follow,tcp,ascii,0 -q`
- **UDP Streams:** `-z follow,udp,ascii,0 -q`
- **HTTP Streams:** `-z follow,http,ascii,0 -q`

## Export Objects

This option helps analysts to extract files from DICOM, HTTP, IMF, SMB and TFTP. The query structure is explained in the table given below.

|   |   |   |   |
|---|---|---|---|
|**Main Parameter**|**Protocol**|**Target Folder**|**Additional Parameter**|
|--export-objects|- DICOM<br>- HTTP<br>- IMF<br>- SMB<br>- TFTP|Target folder to save the files.|-q|

You can filter the packets and follow the streams by using the parameters given below.  

- `--export-objects http,/home/ubuntu/Desktop/extracted-by-tshark -q`

## Credentials

This option helps analysts to detect and collect cleartext credentials from FTP, HTTP, IMAP, POP and SMTP. You can filter the packets and find the cleartext credentials using the parameters below.

- `-z credentials -q`

## Advanced Filter Options

| **Filter**   | **Details**                                                                                                                 | Example                                       |
| ------------ | --------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| **Contains** | - Search a value inside packets.<br>- Case sensitive.<br>- Similar to Wireshark's "find" option.                            | ``http.server contains "Apache"``             |
| **Matches**  | - Search a pattern inside packets.<br>- Supports regex.<br>- Case insensitive.<br>- Complex queries have a margin of error. | ``http.request.method matches "(GET\|POST)"`` |
## Extract Fields

| **Main Filter** | **Target Field** | **Show Field Name** |
| --------------- | ---------------- | ------------------- |
| -T fields       | -e <field name>  | -E header=y         |
```
user@ubuntu$ tshark -r demo.pcapng -T fields -e ip.src -e ip.dst -E header=y -c 5 

ip.src ip.dst 
145.254.160.237 65.208.228.223 
65.208.228.223 145.254.160.237 
145.254.160.237 65.208.228.223 
145.254.160.237 65.208.228.223 
65.208.228.223 145.254.160.237
```
-----------
## Uses cases

#### Extract Hostnames

`tshark -r hostnames.pcapng -T fields -e dhcp.option.hostname`

#### Extract DNS Queries

`tshark -r dns-queries.pcap -T fields -e dns.qry.name | awk NF | sort -r | uniq -c | sort -r`

#### Extract User Agents

`tshark -r user-agents.pcap -T fields -e http.user_agent | awk NF | sort -r | uniq -c | sort -r`

## Examples

What is the total number of HTTP requests sent to the malicious domain jx2-bavuong.com?

`tshark -r directory-curiosity.pcap -Y "http.request.full_uri contains jx2-bavuong.com" -T fields -e http.request.full_uri | wc -l`

What is the IP address associated with the malicious domain jx2-bavuong.com?

`tshark -r <capture_file.pcap> -Y "http.host == jx2-bavuong.com" -T fields -e ip.dst | sort | uniq
`