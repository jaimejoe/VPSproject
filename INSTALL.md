1. Choose VPS provider and your OS(I went with DigitalOcean and Debian)

2. Create droplet

3. if using SSH, can use SSH client (puTTy) key generator to place into the repository
else can use password to authenticate.

4. Through the SSH client, input the IP address of the VPS. If using SSH, under SSH tab > auth
> Credentials, place your saved private key from the key generator

5. Sign in as root, update the packages,install nginx and install git using 
apt update & apt install git

6. Add your github account with git config --global user.name "your username" &
git config --global user.email "your email"

7. make file and give ownership using 
mkdir /var/www/.ssh
chown -R www-data:www-data /var/www/.ssh/

8.Make SSH for github using
sudo -Hu www-data ssh-keygen -t rsa
sudo cat /var/www/.ssh/id_rsa.pub -> the output should be placed in github

9. clone repo as www-data (the nginx user) to the repo directory (in my case, /var/www/html)

cd /var/www

sudo chown -R www-data:www-data /var/www/[site_dir]

sudo su -l www-data -s /bin/bash

git clone git@github.com:[githubuser]/[gitrepo].git /var/www/[site_dir]
- or for branch -
git clone -b [branch_name] git@github.com:[githubuser]/[gitrepo].git /var/www/[site_dir]

exit

10. Setup cronjob to have automatic pulls, the command to edit it is
crontab -e
then add this
*/1 * * * * su -s /bin/sh www-data -c 'cd /var/www/[site-dir] && git pull'

11. Add, commit and push a file to the repo, somewhere else and now the VPS 
will pull it from the repo


Source: https://thecodebeast.com/auto-deploy-git-on-digital-ocean-or-any-other-vps/