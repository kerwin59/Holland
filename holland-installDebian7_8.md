Installing Holland by hand Debian 7/8:
<Thanks to Melissa England - Racker>
************************************
Holland originally developed by Rackspace 

Holland is an Open Source backup framework originally developed by Rackspace and written in Python. It’s goal is to help
facilitate backing up databases with greater configurability, consistency, and ease. Holland currently focuses on MySQL,
however future development will include other database platforms and even non-database related applications. Because of it’s
plugin structure, Holland can be used to backup anything you want by whatever means you want.


Here's the repo:

Add this to your sources:
# vim /etc/apt/sources.list.d/rax.mirror.rackspace.com.list
******************************************************
# Debian
deb http://download.opensuse.org/repositories/home:/holland-backup/Debian_7.0/ ./
**************************

Install key:
*************
curl -s http://download.opensuse.org/repositories/home:/holland-backup/Debian_7.0/Release.key | sudo apt-key add -

Install packages:
*********************
# apt-get update
# apt-get install holland holland-mysqldump
**************************

Configure Holland:
*********************
Adjust to your expectations <ie. I use the path [backup_directory = /var/lib/mysqlbackup] and set the log file>:
# vim /etc/holland/holland.conf

Adjust to your expectations <ie. Frequency of backups, retain #, holland credentials are here also>:
# vim /etc/holland/backupsets/default.conf

Test your config:
# holland bk --dry-run
**************************

Create the cronjob:
***********************
# vim /etc/cron.d/holland
**************************

:~# cat /etc/cron.d/holland

1 3 * * * root /usr/sbin/holland -q bk
**************************************
