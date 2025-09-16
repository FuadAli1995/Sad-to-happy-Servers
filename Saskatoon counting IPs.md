## Notes and solution

## Description
## There's a web server access log file at /home/admin/access.log. The file consists of one line per HTTP request, with the requester's IP address at the beginning of each line. Find what's the IP address that has the most requests in this file

## Let’s see how  file is formatted 

```bash
tail -n 10 /home/admin/access.log
```
## We can then obtain the top 10 most frequent IP addresses accessing the server, sorted by how many requests are made in descending order.

```bash
awk '{print $1}' /home/admin/access.log | sort | uniq -c | sort -nr | head
```

Can then extract the IP with the highest count with the following command

```bash
awk '{print $1}' /home/admin/access.log | sort | uniq -c | sort -nr | head -1 | awk '{print $2}'
```

Can then extract it to file called highestip.txt

```bash
awk '{print $1}' /home/admin/access.log | sort | uniq -c | sort -nr | head -1 | awk '{print $2}' > /home/admin/highestip.txt
```
Now lets verify it

```bash
sha1sum /home/admin/highestip.txt
```

