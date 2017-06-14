## sitecopy for Magento 1.x AND Magento 2.x sites

Script will differentiate whether it is M1 or M2 site, and will adjust accordingly. All commands will be the same regardless of site version.

Generally I would use OO principles and methods to create tools, however, due for the need to upload to each individual server, I have created a script of only one file.

To copy to server, with freeIPA installed simply use `scp sitecopy server.magemojo.com:/tmp`

ssh into server as normal, su as root `sudo su` and copy script to root home `cp /tmp/sitecopy ~`

Although the sitecopy script can be ran from any directory and can use relative paths, I find running from root home and just using absolute paths to be easiest.


### usage: 

#### Create and copy to new dev instance will create new vhost, dns, new database, new database user, and if needed vm user.

*Please note, disk space is not checked, please check disk space first*

If you need a database user that is named separate than the new database you are creating, you can add the flag `--user`, if not then `--db` is all that is necessary and it will create a db user of same name.

`./sitecopy -n --db new_test --domain test.magemojo.io /home/user/public_html/ /home/user/dev/`

or

`./sitecopy -n -v new_db -d dev.magemojo.com /home/user/public_html/ /home/newuser/dev/`

if a separate user directory is specified, a new vhost user will be created with the name of the user directory.

#### Copy to existing dev instance

All that is needed for existing instance is the domain of the dev instance which can be retrieved from domain list in MHM Host Panel.

`./sitecopy -e --domain test.magemojo.io /home/user/public_html /home/user/dev/`

or

`./sitecopy -e -d dev.magemojo.io /home/user/public_html /home/user/dev/`



./sitecopy -h for full help

If you experience any issues or bugs, please report to david@magemojo.com

#### Future planned improvements

flag to make non-interactive mode.
check disk space to ensure space exists for new instance.
enable script to make copies without logging into servers individually. can have on local system and will remotely create dev copies automatically, thus avoiding to have to upload script to server to do a site copy.
