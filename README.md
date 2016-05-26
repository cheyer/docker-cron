# docker-cron
A simple docker container that runs a cron invoking a shell script.

## how to install and use it
Copy the repository and build from the Dockerimage:


`$ sudo docker build --rm -t docker-cron . `


Run the docker container in the background (docker returns the id of the container):


```
$ sudo docker run -t -i -d docker-cron
b149b5e7306dba492558c7024809f13cfbb616cccd0f4020db61bf715f4db836
```

To check if it is running properly, connect to the container using the id and view the logfile. (You may have to wait 2 minutes)

```
$ sudo docker exec -i -t b149b5e7306dba492558c7024809f13cfbb616cccd0f4020db61bf715f4db836 /bin/bash
root@b149b5e7306d:/# cat /var/log/cron.log
Thu May 26 13:11:01 UTC 2016: executed script
Thu May 26 13:12:01 UTC 2016: executed script
```

The cron job is running. Now let's modify the interval and the actual job executed!


## how to modify
To change the interval the cron job is runned, just simply edit the *crontab* file. In default, the job is runned every minute.


`* * * * * root /script.sh`

To change the actual job performed just change the content of the *script.sh* file. In default, the script writes the date into a file located in */var/log/cron.log*.


`echo "$(date): executed script" >> /var/log/cron.log 2>&1`
