# linux-utils

## Crontab

[sudo] apt-get install cron

/etc/init.d/cron start #start cron scheduler

crontab -e  #edit cron job table

# add entry
`* * * * * date > /tmp.txt`

`* * * * * find /path/to/files* -mtime +5 -exec rm {} \;`

`0 0 * * MON find /path/to/files* -mtime +5 -exec rm {} \; #every monday`
