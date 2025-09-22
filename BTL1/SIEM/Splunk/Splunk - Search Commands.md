We'll cover the following commands:

- **Sort**
- **Stats**
- **Table**
- **Uniq**
- **Dedup**

## Sort

Sort is a useful command that allows us to.. well.. sort the events returned to us by our search. For example, if we had a list of logs from a certain event, and we want to put them in chronological order, but not using Splunk's Time column, we could reference a specific field within the log, such as ‘time’ in Fortigate UTM events, and sort them based on this.

Look at the time field in the events below. They're not in order. Also look at the Time column on the left, notice how this doesn't match up with some of them?

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/405b95c88b3326aea7d85e49a6dda50c600f818ded670f99b5bcebf306337ce03d1437674e52962a8eb85ca26c79.png)

So, we can add to the end of our search to sort on the value of the ‘time’ field, and make it ascending, so the oldest event is shown first.

`| sort time asc`

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/cf1637945b170b5ee95b27bc1b0727bbb6bfcda3a6fbd8383214f95a283248d230fdc673e061bf574c91d608e8b1.png)

We can also add count=x after sort to limit the number of results returned. For example, `**| sort limit=2 time asc**` will show us the first two events from our search query, based on the time field. We can also use ‘desc’ if we want to see values ordered in descending value!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a50339fc2811349792ebe0d72ac289b0e4f7d092ce1c864309319bb7e33fbaff8d3da6fce765aeb36db2de62b13e.png)
## Stats

We can use the Stats command to provide statistics about the results from our search query. In the below example, we're looking at Fortigate UTM logs from a specific date, and have got a list of how many times (count) an IP value is present in the ‘srcip’ field.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/6ead6679cfad49a9017342198c55a6253150290c1da449a6d066f7de070526ff3831e6400e95416887b3e8ccbff2.png)

If we wanted to see the most frequent IP at the top, what can we do? Combine it with a Sort command!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/849805e26c404e65a9933f2aa1c9f303188304b5a46329f0d2f2ad8578bad2300b71ed300cca951f013686bddda7.png)
## Table

We can use the Table command to create a custom table of the data we want to display, and hide everything else. Let's go through an example. Here's on raw log from our search query. We only care about the date, time, srcip, dstport, action, and msg fields.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/6b87b8d0b34e257fd61fea40fd244701f7e097afc5efa87b15f68583614996d8d91b8765dc7589926a816b60f62d.png)

We can add the following to the end of our search query:

`| table date, time, srcip, dstport, action, msg`

Now it's much easier to look at the information we care about, and we can use the column headings for filtering!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c6b571f6d9d308d536003d7638ded029203f24bf96caa70cfdd8109a1b0f911736493b0cf9a9905637b9d9e884df.png)

# Uniq / dedup

The Uniq command can be used to retrieve unique values from our search results. If we wanted to see how many unique IP addresses there are in our logs, we can use Table to only display the srcip field, then perform uniq on the table:

`| table srcip | uniq`

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/6bcbbd970554aa20125e7709fd5cbed55dda8cf8eb6204af6955bbcfdfea1792270c308438d4fcfdde5935ae4b49.png)

In some cases uniq doesn't seem to work (maybe it's just us!), but we can alternatively use the dedup command to de-duplicate results. Combining this with a table, we can check what the various ‘action’ values are for Fortigate UTM logs:

`| table action | dedup action`

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/eb335bafe2f7e3b286890029fbd591183b51b8416abd5aa02e55f9ba18e0a8251c63714aa8092823eaf3d383d7e9.png)

---