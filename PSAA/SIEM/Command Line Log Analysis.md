`ls -lh access.log` // time and permission
`wc access.log` // calculate number of strings, words, bytes
`wc -l access.log` // calculate number of strings

`head access.log -n 1` //output only 1 line (first event)
`tail access.log -n 1` //output only 1 last line (last event)

----

`more access.log` // cat file to the terminal - more good view, than just "cat"
`less access.log` // cat file to the terminal - more readble
pres "q" to quit

---

![[Pasted image 20250128153819.png]]
`cut access.log -d " " -f 1 | sort` // cat only IPs
`cut access.log -d " " -f 1 | sort | uniq -c | sort -nr` // count only uniq IPs

`cut -d "\"" -f 6 access.log` // it will cat a User Agent strings only
`cut -d "\"" -f 6 access.log | sort | uniq -c | sort -nr` // it will cat count for all User Agent

`grep "Mozilla/5.0 (Hydra)" access.log`
![[Pasted image 20250128154652.png]]

`grep "Mozilla/5.0 (Hydra)" access.log | awk '{print $1}'` // it will extracted only IPs from previous command and screen, that tied to "Mozilla/5.0 (Hydra)" .

`grep "Mozilla/5.0 (Hydra)" access.log | awk '{print $1}' | sort | uniq -c`

------

`grep "Mozilla/5.0 (Hydra)" access.log | awk '$9 > 200'` // show only logs with code > 200. Fx 302 - Redirect.

------

## Just Grep

`grep "404" access.log`

`grep -n "404" access.log` //also shows number of packets (line)

Use grep signtures to find SQL injection (' ; .) , path traversal (../ ../../), XSS (<>) etc

-----

# Jason format logs

`jq . events.json` // standard show

`jq 'length' events.json` // counts events in total

`jq 'map(.event)' events.json`

`jq '.[] | select(.event.PROCESS_ID == 3532)' events.json`

![[Pasted image 20250128191033.png]]

`jq '.[] | select(.event.PROCESS_ID == 3532) | .event.FILE_PATH' events.json` //show full file path from event

`jq '.[] | select(.event.PROCESS_ID == 3532) | .event.PARENT.FILE_PATH' events.json` //show full parent file path from event

`jq '.[] | select(.event.PROCESS_ID == 3532) | .event.HASH' events.json` 

`jq '.[] | select(.event.PROCESS_ID == 3532) | .event.PARENT.HASH' events.json` 

`jq '.[] | select(.event.PROCESS_ID == 3532) | .event.PROCESS_ID' events.json` 

## Using automation alert for json

Use tool that generates alert (you can adjust what kind of alert you want) to your full events .json file for exaple:

![[Pasted image 20250128191631.png]]