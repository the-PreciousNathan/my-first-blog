# Hosting a Static Website on AWS EC2 using Nginx 
### Welcome to my Blog!


There are days when learning feels theoretical and then there are days when things finally become real.

This was one of those days.

Before now, I had heard a lot about things like web servers, Elastic IP, AMIs and EC2 instances, but they always felt like distant cloud terms. I understood the definitions, but I couldn’t really picture how they worked together in real life.

Good news! I finally did.

Instead of just hearing about infrastructure, I actually saw how a machine becomes a server, how that server becomes a web server, and how a web server ends up hosting a real website.

* * *

## First Realization: A Server is Just a Computer

One of the first things that clicked was understanding that a server is not some mysterious machine. A server is simply a computer that responds to requests by sending back files or resources. Any computer can be configured to act as a server or a client, the difference lies in what role it is assigned.

But then comes the important distinction: a web server is not the machine itself. A web server is software that responds to client requests over the internet and delivers web pages.

So the machine is the server, and the software determines the service, and depending on what you install, your server can become:

A web server, an email server, a DNS server, a database server, and a DHCP server.

* * *

## What AWS Does For You

AWS made this idea even easier to understand. So now, instead of buying physical hardware, AWS provides existing servers that you can rent and this helps eliminate capital expenditure.

AWS owns and maintains the infrastructure you have rented and you simply operate what runs on it and this is where EC2 comes in.

EC2 allows you to **create** and **manage** virtual servers in the cloud, so when I launched an EC2 instance, I had essentially rented a computer but at that point, it was still just a machine.

* * *

## Connecting To The Server

To configure the instance, I connected to it using SSH, but first, you want to log into your AWS console, open the **EC2** service, and create an instance. Now you really want to **c*reate a new keypair,*** especially if you can't remember the old keypair you want to associate with your instance. We'll need it to SSH into the instance you just created.

Click the checkbox of the instance and click on connect. This is where we get open our terminal.

cd into your downloads folder where the keypair is and paste the example code on your aws instance connect page. It should look like this

`ssh -i "my-blogpost-keypair.pem" ubuntu@ec2-3-238-162-165.compute-1.amazonaws.com`

You should now be in your instance via the terminal.


* * *

## Preparing the Server

Before installing anything, I updated the operating system. You'd like to update your operating system first. This is a best practice because installing software on an outdated system can introduce security risks and compatibility issues.

`sudo yum update`

`sudo apt update`

yum for Linux, apt for Ubuntu

Then we install Nginx.

`sudo yum install nginx`

To prevent any issues, you want to run some code

1.  To check the connection: `curl localhost`
    
2.  To check the status: `sudo systemctl status nginx`
    
3.  To start it: `sudo systemctl start nginx`
    
4.  To check if it's installed: `nginx -v`
    

A bonus hack to ensure things run smoothly is to enable port 80 on your security group inbound rule. (you also want to take out the 's' in 'https' when you do that.) *You are welcome*.

* * *

## Hosting Your Static Website

Nginx is a web server software, so the EC2 instance stopped being just a server and is now a web server capable of:

*   Storing website files
    
*   Processing requests
    
*   Delivering web pages
    

Now we can host our static website. We're working from the terminal and I'm using a template from open source in Git. Copy the link to the source code, make sure you have Git installed (`git --version`)

Go ahead to clone it `git clone <link>`

```shell
B
ls 
cd /var/www/html/ 
ls
```

Where /var/www/html/ is the root folder of nginx and has the display files and folders there.

You'd want to `sudo mv <downloaded folder> /var/www/html/`

You're almost there...

Now, you can copy the downloaded folder name, e.g.,

***beginner-html-site,*** and paste it right beside your ip address, and Voila!

Your website is running on your Nginx server.

Try this method on your EC2 instance and let me know how it goes.



***Want to go further? In the next post I’ll cover:***

*   ***How to configure CloudFront with an EC2/nginx origin***
    
*   ***TLS (ACM) and custom domains for CloudFront***
    
*   ***Cache strategies, invalidations, and CI/CD for fast rollouts***
