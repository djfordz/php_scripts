# WARNING
### Although every precaution and check has been made to make this script as safe as possible, there is always corner cases. This script should never harm the live site, and all precautions have been made for this, but it is never 100%. Use at your own risk!

#### There may be corner cases with the copied site, and manual methods may need to be employed to ensure the copied site works correctly, such as this script can only set a single domain in the database, if there are multidomains the customer wants set, these will have to be added manually. If you are not comfortable doing this, do not use this script!

## sitecopy for Magento 1.x AND Magento 2.x sites

Script will differentiate whether it is M1 or M2 site, and will adjust accordingly. All commands will be the same regardless of site version.

Generally I would use OO principles and methods to create tools, however, due for the need to upload to each individual server, I have created a script of only one file.

ssh into server as normal, su as root `sudo su`

#### To copy to server, simply use `wget -c https://raw.github.com/djfordz/php_scripts/master/sitecopy`

make script executable `chmod +x sitecopy`


### usage: 

Although the sitecopy script can be ran from any directory and can use relative paths, I find running from root home and just using absolute paths to be easiest.

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

Use flag -i for non-interactive mode. *note: you will not get any prompt when deleting files.*

./sitecopy -h for full help

If you want to create a new database instead of importing into existing when copying to an existing instance, you can add the --db or -v flag and a new database name, this overrides getting the database creds from local.xml or env.php. example:

`./sitecopy -e -d dev.magemojo.io -v new_db /home/user/old/ /home/user/new/

Now instead of emptying tables of existing database, it will just create a new database and user.

*If you experience any issues or bugs, please report to david@magemojo.com*

#### Future planned improvements
1  check disk space to ensure space exists for new instance.
2  ssh server to server copy.
