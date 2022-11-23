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
