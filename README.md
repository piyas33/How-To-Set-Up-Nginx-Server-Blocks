# How-To-Set-Up-Nginx-Server-Blocks
How To Set Up Nginx Server Blocks

###  Installing Nginx
```
sudo apt update
sudo apt install nginx
```
### Create Project Folder
```
cd /var/www
sudo mkdir mywebsite.com
```
For testing purposes, setup the default html pages. (or you can past your full project file `/var/www/mywebsite.com` directory.)
```
nano /var/www/mywebsite.com/index.html
```
And paste: 
```html
<html>
    <head>
        <title>Welcome to mywebsite.com!</title>
    </head>
    <body>
        <h1>Success! The mywebsite.com working</h1>
    </body>
</html>
```
To avoid any permission issues, change the ownership of the domain document root directory to the Nginx user (www-data):
```
sudo chown -R www-data: /var/www/mywebsite.com
```
### Configure nginx
```
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/mywebsite.com
sudo nano /etc/nginx/sites-available/mywebsite.com
```
Edit the `root` and `server_name`.


```root```  where we have placed our .html file.

```index```  specify file available when visiting root directory of site.

```server_name```  any real domain(ex. mywebsite.com) or ip address(ex. 127.0.0.1).

```listen```  port number.You can change it if you would like to.


```
server {
       listen 81;
       listen [::]:81;

       server_name 127.0.0.1;

       root /var/www/mywebsite.com;
       index index.html;

       location / {
               try_files $uri $uri/ =404;
       }
}

```
### Restart the Nginx service for the changes to take effect:
```
sudo service nginx restart
```

### Browse your site in your browser
```
127.0.0.1:81
```
