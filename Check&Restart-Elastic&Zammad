#!/bin/bash
### Author: Mayur G. Chavhan 8788016553

###Service and Email
service=Elasticsearch
elserv=$(/etc/init.d/elasticsearch status | grep active | awk '{print $2}')
service2=zammad
zamserv=$(service $service2 status | grep active | awk '{print $2}')
#zamserv=$(ps -ef | grep -v grep | grep $service2 | wc -l)

email=mail@gmail.com

###
host=`hostname -f`
if [ $elserv == active ]
then
echo -e "\n $service is already running"
subject="$service at $host has been started"
echo "$service at $host wasn't running and has been started" | mail -s "$subject" $email
else
/etc/init.d/elasticsearch start

echo -ne '\n ########          (50%)\r'

echo -e "\n Zammad search index will starting to rebuild... \n"

sleep 2m

zammad run rake searchindex:rebuild

sleep 1m
echo -ne '\n #######################   (100%)\r'
echo -ne '\n'

#subject="$service at $host is not running"
#echo "$service at $host is stopped and cannot be started!!!" | mail -s "$subject" $email
fi

if [ $zamserv == "active" ]

then
echo -e "\n $service2 is already running \n"

else

echo -e "\n $service2 is starting now \n"

service $service2 start

echo -e "\n Zammad is started \n"

fi
