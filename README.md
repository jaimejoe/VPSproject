# VPSproject
The scenario is a auto-deployment of websites to a VPS using git. So, the VPS would 
what files a github repository had, and pull from it automatically. The ways to do this
were either using php, cronjob or a bash script. Out of all of them, I ended up using 
cron as webhooks as a problem with the php file, and while bash is fairly simple, 
the cron command was much faster to implement than bash. For the selection of the VPS,
DigitalOcean seemed like the good choice, since it was recommended in the slides and 
the tutorial I followed used it to. Setup with it is fairly simple and price is a bargain.
To connect to the VPS, I initially intended using terminal on a VM, however I was 
recommended to use an SSH client, so I settled for what DigitalOcean recommended me,
which is puTTy. I directly am able to access the VPS with no overhead.
