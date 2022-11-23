# 2420_week12_Lab
# Team Members
Sandeep Kaur

Jacob Lloyd

# Description
This is a guide on how to install NGINX on a digital ocean droplet with a firewall.
## Step 0
* Do the setup for the droplets by following the video : <a href="https://vimeo.com/758870226/f75da348fc?embedded=true&source=vimeo_logo&owner=17609105" target="_blank">DO Setup</a>
* After following the video you will have 1 regular user which is allowed to ssh into the droplet while the root user will not have access to the droplet.

## Step 1
Install NGINX on the server by following these instructions:
* You will need to update and upgrade your server files using ```sudo apt update && sudo apt upgrade ```

![update upgrade](https://user-images.githubusercontent.com/97915467/203537214-a39b61ad-25b6-4a87-84df-0a6d3cb8982c.JPG)

* After that you will need to install nginx using ``` sudo apt install nginx ```

![nginx_install](https://user-images.githubusercontent.com/97915467/203537241-037f5305-5b10-4932-9cda-08baceebed01.JPG)

* After installing nginx check the status using ``` sudo systemctl status nginx ```

![statusnginx](https://user-images.githubusercontent.com/97915467/203606313-a7870aef-047b-462f-8c60-e812d7195f9d.JPG)

## Step 2
* Create a simple, but complete HTML document to serve. Your file should be named **index.html**
``` <!DOCTYPE html>
<head>
        <title> ACIT 2420 Week 12</title>
        <style>
                body {
                        background-color: #2D2D2D;
                }

                h1 {
                        color: #C26356;
                        font-size: 30px;
                        font-family: Menlo, Monaco, fixed-width;
                }

                p {
                        color: White;
                        font-family: "Source Code Pro", Menlo, Monaco, fixed-width;
                }
        </style>
</head>
<body>
        <h1>Hello Everyone</h1>
        <p>This is a webpage created for Week 12 lab for ACIT 2420 by <b>Sandeep Kaur & Jacob Lloyd</b> </p>
</body>
</html> 
```
## Step 3
* Write an nginx server block to serve your HTML document from step 2.
```
server {
        listen 80;
        listen [::]:80;

        root /var/www/147.182.243.201/html; # Change the ip address to your droplets ip address
        index index.html;

        server_name 147.182.243.201; # Change the ip address to your droplets ip address

        location / {
                try_files $uri $uri/ =404;
        }
}
```

## Step 4
* Upload your files to your server.
* To upload your files using sftp. 
``` sftp -i ~/.ssh/id_rsa web-one@147.182.243.201 ```
* After it connects to the servers ip address you can use 
``` put -r index.html ```
``` put -r 147.182.243.201 ```
* This will put both the files in the droplet.
![put_files](https://user-images.githubusercontent.com/97915467/203539910-d13577c9-dcbe-452d-9660-977349c20ef9.JPG)

* Move the files to the appropriate directories. 
* Index.html file will be moved to /var/www/147.182.243.201/html using  ``` sudo mv index.html /var/www/147.182.243.201/html/ ```
* 147.182.243.201 server blovk will be moved to /etc/nginx/sites-available using ``` sudo mv 147.182.243.201 /etc/nginx/sites-available/ ```
* ![mv_index](https://user-images.githubusercontent.com/97915467/203540179-04d9a549-2714-4aa5-8768-e7c12d2fca92.JPG)
![mv_server](https://user-images.githubusercontent.com/97915467/203540221-e1162285-7670-427e-9dbe-5cdcadb1c304.JPG)

* you can create a soft link to your new server block in sites-enabled ``` sudo ln -s /etc/nginx/sites-available/your_ip /etc/nginx/sites-enabled/` ```
![soft_link](https://user-images.githubusercontent.com/97915467/203542273-e01ddaf7-1dcb-48ab-8e71-963b7fd9e581.JPG)


## Step 5
* Start or restart your service.
* Restart nginx using ``` sudo systemctl restart nginx ```
![restart_nginx](https://user-images.githubusercontent.com/97915467/203541421-ec033849-512b-484d-9171-af855d2ecd73.JPG)

## Step 6
* Check to see if your document is being served by visiting your servers ip address
![website_html](https://user-images.githubusercontent.com/97915467/203541517-27c86e51-53fa-4dd9-8360-6222c05a513a.JPG)

## Step 7 
* Setup a firewall using UFW. Allow incoming HTTP and SSH connections. 

```  sudo ufw enable ```

```  sudo ufw status ```

``` sudo ufw allow OpenSSH ```

``` sudo ufw allow 'Nginx HTTP' ```

![ufw](https://user-images.githubusercontent.com/97915467/203541706-fabd3568-597c-4a49-b2f2-67b98e5a2b2f.JPG)
