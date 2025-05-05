**GOAL**

The goal of this project is to deploy a static website for Elite Corporation on an AWS EC2 instance using Apache2 as the web server, secured with HTTPS via Certbot. The website includes a company banner ("Welcome to Elite Corporation"), sections for About Us, Services, and Contact, and is styled with CSS for a clean, modern look. The project involves setting up an Ubuntu server, installing Apache2, deploying the website to /var/www/html, configuring DNS for public accessibility, and securing the site with a Let’s Encrypt SSL certificate. This documentation outlines the step-by-step process I followed.

**TOOLS AND EXPECTED FUNCTIONS**


The tools I used for this project are:

1) **LINUX**  
   Linux (Ubuntu 20.04) is the operating system for my EC2 instance. It provides a stable and secure environment for hosting the website, coordinating interactions between Apache2 (the web server) and Certbot (for SSL). It’s key to deploying and managing the website efficiently.

2) **APACHE2**  
   Apache2 is the open-source web server software that handles client requests and serves the static website. It processes HTTP requests, delivering HTML and CSS content to users’ browsers. Apache2 ensures the Elite Corporation website is accessible and performs reliably.

3) **CERTBOT**  
   Certbot, paired with Let’s Encrypt, automates the process of obtaining and installing SSL certificates to enable HTTPS. It interacts with Apache2 to secure the website, ensuring encrypted communication between the server and users, despite challenges with DNS validation.

4) **DNS (FREENOM)**  
   Freenom provides the free domain, allowing users to access the website via a custom URL instead of an IP address. It manages DNS records to map the domain to the EC2 instance, though propagation delays posed challenges.

## CONCEPTS COVERED

AWS (EC2, Security Groups), Linux (Ubuntu), Apache2, HTML/CSS, Certbot/Let’s Encrypt, DNS (Freenom, A records), SSL/TLS, Networking (ports, firewall rules), Troubleshooting (NXDOMAIN errors)

## PROJECT TASK

| S/N | Tasks                                      |
|-----|--------------------------------------------|
| 1   | Launch an Ubuntu server on AWS EC2         |
| 2   | Install and configure Apache2              |
| 3   | Deploy the Elite Corporation website       |
| 4   | Set up DNS for `elitecorp.ml`             |
| 5   | Secure the site with Certbot for HTTPS     |
| 6   | Validate the website’s accessibility       |

## DOCUMENTATION

### TASK-1: DEPLOY AN UBUNTU SERVER

- I launched an Ubuntu server named `EliteCorp-WebServer` on AWS EC2 to host my website, as shown below.  

![Image](https://github.com/user-attachments/assets/04e53f87-2ea5-48a9-8dce-b7b0b3ffc44f)


- I selected my `EliteCorp-WebServer` instance and proceeded to set inbound rules under the security group. I clicked on Security and selected the Security group.  

  
![Image](https://github.com/user-attachments/assets/dd40973a-1524-4430-90e2-fd22ff605d13)



- I opened my terminal and connected to my Ubuntu server via SSH using the instance’s public IP.

chmod 400 elitecorp-key.pem
$  ssh -i elitecorp-key.pem ubuntu@13.50.252.255


![Image](https://github.com/user-attachments/assets/d587237b-01f0-4a67-a888-e634ed7d17fe)



**TASK-2: SETUP APACHE2 ON THE SERVER**

- I installed and configured Apache2 to serve the static website.

Update Packages: sudo apt update 
Install Apache2: sudo apt install apache2 -y
 
![Image](https://github.com/user-attachments/assets/c3bc5855-6c62-4f70-bb5d-4bcd0488a2d9)
![Image](https://github.com/user-attachments/assets/aa02bb6c-91a6-4a75-be05-872bddbd3335)


- I executed sudo systemctl enable apache2n and sudo systemctl status apache2 to enable Apache to start on boot and confirm status respectively.

- Confirmed active (running) status.

![Image](https://github.com/user-attachments/assets/5ed3a931-9dc5-49d0-bda1-c848861d28cd)



- I checked if Apache2 was serving content by executing curl http://localhost:80

- Returned the default Apache2 HTML page.

![Image](https://github.com/user-attachments/assets/4b73b5b1-ec61-4906-9a59-7e362a2900cb)



- Opened a browser and navigated to http://13.50.252.255. I saw the default Apache2 Ubuntu page, confirming public accessibility.

![Image](https://github.com/user-attachments/assets/fec757eb-0d85-4e7f-a816-46579f6fdf79)


- Adjusted ownership and permissions for /var/www/html: 

sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html


##TASK-3: DEPLOY THE STATIC WEBSITE

- I created and deployed the Elite Corporation static website to /var/www/html.

- Create index.html:

- Edited the website file by executing sudo vim /var/www/html/index.html

- Pasted the HTML/CSS code for the Elite Corporation website, featuring:

- Banner: “Welcome to Elite Corporation” with a tagline.

- Sections: About Us, Services (grid layout), Contact.

![Image](https://github.com/user-attachments/assets/3208e3d9-baea-4208-9ee8-10bd5d5c6acc)



- Set File Permissions:

sudo chown www-data:www-data /var/www/html/index.html
sudo chmod 644 /var/www/html/index.html

- Test Website:

- I reloaded Apache2 by executing sudo systemctl reload apache2 and i visited http://3.123.45.67 in a browser.

- I confirmed the Elite Corporation website loaded with the tech blue background, navigation, and sections.

![Image](https://github.com/user-attachments/assets/9b1cbf81-9047-4e07-9e95-9596b035488a)



