#### During the project I encountered an error involving CORS(Cross origin resource sharing).Firstly what is cors?

##### CORS is an HTTP header-based mechanism that allows the server to indicate any other domain, scheme, or port origins and enables them to be loaded.

How to solve the CORS error for the angular app.

###### 1) Install plugin moesif CORS extension(Local development solutiom)
The quickest fix you can make is to install the moesif CORS extension.Once installed,click it in your browser to activate the extension. Make sure the icon’s label goes from “off”.
NB:This is a temporary fix and not a very good business decision as all clients requesting data from the server should not install a plugin to be able to get access to an api resource.
The plugin only works for local development.

###### 2) Add suitable CORS header to backend api server
######CORS on Apache Server
To add the CORS authorization to the header using Apache (or, Apache2), simply add the following lines in your server config (usually located in /etc/apache2/apache2.conf file), or within a .htaccess file:

<Directory /var/www/my-callback-url-path>
     Order Allow,Deny
     Allow from all
     AllowOverride all
     Header add Access-Control-Allow-Headers "origin, x-requested-with, content-type, authorization"
     Header add Access-Control-Allow-Methods "GET, POST, OPTIONS"
     Header set Access-Control-Allow-Origin "https://stagegateway.eko.in"
</Directory>


Add/activate module by running the command: a2enmod headers
Check that your changes are correct by running the command: apachectl -t
Reload Apache: sudo service apache2 reload
Check more details here



