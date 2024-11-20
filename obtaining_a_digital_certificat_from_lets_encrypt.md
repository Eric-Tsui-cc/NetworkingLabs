[[File:lets_encrypt.png|right|thumb|x450px|alt#The Let's Encrypt Website|The Let's Encrypt Website]]
Much of this information is sourced from: https://letsencrypt.org/getting-started/

## Pre-requisites ##

Before starting to ensure that you have an A record pointing to the IP address of your server. To verify that you have met this prerequisite, you should be able to ssh from your local machine. For example, the following should be successful

	ssh -i pemkey.pem ubuntu@[yourdomain-name-goes-here.com]

I will also assume that you are running the Apache web server and have current access. You could use a web browser or from the CLI you could:

	wget http://[yourdomain-name-goes-here.com]

If these tests fail, go back to the Amazon EC2 server lab and the DNS lab and make sure these tests work before you proceed. Check that the firewall in your Amazon machine has port 22, 80 and 443 open.

## Obtaining your digital certificate from Let's Encrypt ##

You should, for testing purposes have TCP port 22, 80 and 443 available through the firewall. Once you have tested that your website is working over HTTP (port 80), it is time to get a certificate and enable it over HTTPS (port 443). Go to: 

	https://certbot.eff.org/

Select I'm using "Apache" on "Ubuntu 20.04". This will provide you with the instructions, which I have re-provided below. These instructions add additional repositories that will allow your Ubuntu instance to download the correct packages. 

Install snapd

	sudo snap install core
	sudo snap refresh core

Remove certbot-auto and any Certbot OS packages
	sudo apt remove certbot

If you previously used Certbot through the certbot-auto script, you should also remove its installation by following the instructions here.

Install Certbot

	sudo snap install --classic certbot

Execute the following instruction on the command line on the machine to ensure that the certbot command can be run.

	sudo ln -s /snap/bin/certbot /usr/bin/certbot
	sudo certbot --apache

You should not need to run Certbot again, unless you change your configuration. You can test automatic renewal for your certificates by running this command:

	sudo certbot renew --dry-run

To confirm that your site is set up properly, visit your website in your browser and look for the lock icon. Click on the lock icon to see if you can tell who issued the certificate.

