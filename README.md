# VPSproject

###Description
The scenario is an auto-deployment of websites to a VPS using git. So, the VPS would check
what files a github repository had, and pull from it automatically using a cronjob which checks every minute. 
VPS is from DigitalOcean and I connect to it using puTTy, an SSH client. For the selection of the VPS,
DigitalOcean seemed like the good choice, since it was recommended in the slides and 
the tutorial I followed used it to. Setup with it is fairly simple and price is a bargain.
To connect to the VPS, I initially intended using terminal on a VM, however I was 
recommended to use an SSH client, so I settled for what DigitalOcean recommended me,
which is puTTy. I directly am able to access the VPS with no overhead. All commands are done through puTTy. Done for UNIX course 2024.

Resources downloaded/used: 
 -https://thecodebeast.com/auto-deploy-git-on-digital-ocean-or-any-other-vps/#google_vignette
 -https://try.digitalocean.com/cloud/?utm_campaign=amer_brand_kw_en_cpc&utm_adgroup=digitalocean_droplet_exact&_keyword=digitalocean%20vps&_device=c&_adposition=&utm_content=conversion&utm_medium=cpc&utm_source=google&gad_source=1&gclid=CjwKCAjwr7ayBhAPEiwA6EIGxKyAxCJ-cpt6k3ylehdXVfL0Pls1IBa8kGFXIwsa7Oc_wqW__hLWjBoCaZkQAvD_BwE
 -https://www.putty.org
 



###Installation
Sign in and get a VPS at 
https://try.digitalocean.com/cloud/?utm_campaign=amer_brand_kw_en_cpc&utm_adgroup=digitalocean_droplet_exact&_keyword=digitalocean%20vps&_device=c&_adposition=&utm_content=conversion&utm_medium=cpc&utm_source=google&gad_source=1&gclid=CjwKCAjwr7ayBhAPEiwA6EIGxKyAxCJ-cpt6k3ylehdXVfL0Pls1IBa8kGFXIwsa7Oc_wqW__hLWjBoCaZkQAvD_BwE


Installs needed
	$apt update
	$apt install git
	$apt install nginx
	
Configure GitHub account
	$git config --global user.name "your username" 
	$git config --global user.email "your email"

Directory to store keys/ owndership to www-data(nginx) user
	$mkdir /var/www/.ssh
	$chown -R www-data:www-data

Generate RSA keys
	$sudo -Hu www-data ssh-keygen -t rsa
	$sudo cat /var/www/.ssh/id_rsa.pub 

Place keys in github

Cloning repo as nginx user

	$cd /var/www

	$sudo chown -R www-data:www-data /var/www/[site_dir]

	$sudo su -l www-data -s /bin/bash

	$git clone git@github.com:[githubuser]/[gitrepo].git /var/www/[site_dir]
- or for branch -
	$git clone -b [branch_name] git@github.com:[githubuser]/[gitrepo].git /var/www/[site_dir]

exit

Cronjob to automatically pull
	$crontab -e
	*/1 * * * * su -s /bin/sh www-data -c 'cd /var/www/[site-dir] && git pull'




