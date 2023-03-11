## Starting the BNPL WEB PROJECT

To start the bnpl project i was given my difital ocean cloud server access.This server is where the app will be deploy.I have been given one server as the project is just at its beginning.I wiil later on be given 2 more server so I can have the testing,staging and production environments.

### Configuring my digital ocean server and my project in general

#### Configuring a virtual host on apache2

To configure a VH on the server I had to : 

##### 1. install apache2 on the ubuntu server using the command:

###### sudo apt update
###### sudo apt install apache2

##### 2. Configure a virtual host:

###### Create a folder for the project in the directory /var/www/html.
###### Go to the directory /etc/apache2/sites-available/ and create a config file with name your_domain_name.conf using the command sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/your_domain_name.conf to create a copy of the default apache site conf file.
###### modify the conf file with ServerAdmin your email,ServerName your domain name,ServerAlias your server name and root the directory with the index.html of your project.
###### Activate the site using the command sudo a2ensite your_domain_name.conf.
###### Finally restart apache using the command service apache2 reload.


#### Configuring a bitbucket pipeline for Angular application deployment.

##### 1. Create a bitbucket.yml file which contains the config for your pipeline.Can use the template below

![.yml file](https://github.com/kamdem-arielle/BNPL-WEB/blob/2d2db47a5daba6d8fd80598ad30e91cead632e0a/assets/bitbucket.png)

