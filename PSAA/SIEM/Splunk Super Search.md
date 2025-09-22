U can download your .csv file directly to splunk. Than in the search filter use `index="name_events.csv"`

## Keyword search

`index="name_events.csv" failed` // failed is just a word that grep something

`index="name_events.csv" "jdo,login"` // search for something specific included space and coma.

`index="name_events.csv" fail*` // search for something with this part.
`index="name_events.csv" *fail` // search for something with this part.
`index="name_events.csv" 12:*:00` // search for something with this time, just minute can change.

## Field Search

`index="name_events.csv" file!="login.php"` // use filter from left column and just add "!" before "=" to exclude it from search.

`index="name_events.csv" status>200` // use filter from left column and just add ">", ">=" or "<" if its countable field.

`index="name_events.csv" clientip=100.*.*.*`

Use: `AND`, `AND NOT`, `OR`

Use `earliest=-1d` or `earliest=-1h` etc. //search for 1 day or 1 hour eralier of specific time
Use `latest=+1d` or `latest=+1h` etc. //search for 1 day or 1 hour later of specific time
Use this with absolute value of date:

![[Pasted image 20250128213814.png]]

## Organizing output Command

### sort

`index="http_sample" | sort req_time` // sort base on the **req_time** field. You can change **req_time** for any field.

### stats 

`index="http_sample" | stats count by clientip` // just extract concretic field for statisctic and count.

![[Pasted image 20250128214737.png]]

`index="http_sample" | stats count by clientip | sort -count | head 5` //top 5 max used ip in http_sample.
`index="http_sample" | stats count by clientip | sort -count | tail 5` //last 5 max used ip in http_sample.

### table

`index="http_sample" | table _time, clientip, method, uri, useragent` // the same as stats, but you can specify many fields that you want to be showed

![[Pasted image 20250128215213.png]]

### dedup (similar to 'uniq')

remove duplicated events based on the specific field.

`index="http_sample" | table _time, clientip, method, uri, useragent | dedup useragent` // the same as stats, but you can specify many fields that you want to be showed

### rename

just can rename the column

`index="http_sample" | table _time, clientip, method, uri, useragent | rename useragent as "USER AGENT"`

### 'top' and 'rare'

`index="http_sample" | table _time, clientip, method, uri, useragent | top limit=5 useragent` //top 5 values based on the specific field

![[Pasted image 20250128215646.png]]

`index="http_sample" | table _time, clientip, method, uri, useragent | rare limit=5 useragent` //Oposite. top 5 rarest values based on the specific field

### chart

`index="http_sample" | chart count by status` //show diagrams-visualisation

![[Pasted image 20250128215900.png]]
![[Pasted image 20250128220035.png]]

### iplocation

`index="http_sample" | iplocation clientip | table _time, Country, City, uri`

![[Pasted image 20250128220346.png]]

# Report

its super easy to make a report with your search query. Go to Search Bar, On the right - "Save As -> Report"

# Generating Alerts

You can also save it as "alert" to trigger the condition in real time!!

![[Pasted image 20250129100548.png]]

# Generate a Dashboard!

![[Pasted image 20250129101024.png]]

# MAKE THIS RULE:

when someone clear the logs, make an alert
![[Pasted image 20250129115348.png]]

Idea - generete a list of alerts for splunk.