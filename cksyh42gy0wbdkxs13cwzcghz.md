## How to setup a https server in Elastic Beanstalk (The Cheap Way)?

Yeah.. I know, the title is a mouth full. To be honest, this is a very specific and niche usecase I faced and found no condensed resources. So, here is my attempt making one!! I hope this article helps you in the journey towards learning new things!!

# Objectives

With this article, I just aim to setup a server with following properties :

- HTTPS - Secure Web Server.
- Auto renewal of SSL certificates (from let's encrypt).
- Elastic beanstalk with single instance mode (no load balancer)
- Automatic Continous Deployment from github. **Coming Up in the next Article**

Since This might be a lot to take in, I'll write a seperate article on Continous Deployment.

I followed these steps for a project that had minimum requirements and tight budget constraints. I **do not** recommend this for bigger projects where scale matters a lot.

# TLDR;

If you know elastic beanstalk and just want to know how to setup SSL, refer to this [source code from vahiwe](https://github.com/vahiwe/Elastic-Beanstalk-Single-Instance-SSL) and copy the `.platform` and `.ebextensions` folders into your application.  Source of this code is this [awesome article by vahiwe](https://aws.plainenglish.io/setup-ssl-https-on-elastic-beanstalk-single-instance-environment-d748ea04437d).

Do not forget to set `DOMAIN_LINK` and `EMAIL_LINK` environment variables for the domain you want ssl certificate for and the email associated with it respectively.

# Why bother reading this?

Although you might not face these specific conditions, this article will contain stuff that I didn't understand before this. Sometimes, we treat things like SSL, Nginx etc as black boxes that just do stuff, but **The craft of engineering is about understanding the parts and making a better whole.**

# Setting up AWS Elastic Beanstalk

## What is Elastic Beanstalk?

Elastic Beanstalk or EB is an easy to use service from AWS for deploying and scaling web applications. It supports both uploading your code manually and stuff like CD by using AWS Code Deploy. It manages various things like creating new EC2 instances automatically, deploying your code to the server, starting your applications and much **much** more.

There are no extra charges for EB, you just pay for what you use e.g. EC2 instances, Load Balancers, CodeDeploy Pipelines etc.

## How Do I setup one?

Setting up a basic EB project is simple.

### Create new EB Environment

In your AWS console, go to elastic beanstalk option and click "Create new Application"
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630308231020/7FPW64f9p.png)
Fill everything up and click "Configure More Options"
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630308286316/lgUygNAoc.png)
Make sure, the presets selects "Single Instance" and the Load Balancer Option says "This Configuration does not contain a load balancer"
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630308313605/ERe3BzZE8.png)
Select all other options that you require like Databases, Software Environment Variables etc and Click "Create App"
This will create a default environment for you.
Congrats, you now have a single instance EB application online. But it doesn't have your app. 😕

## Configure your application code for Elastic Beanstalk to support HTTPS

This step will be the quickest to do but the weirdest to understand.

### A little Background

Elastic Beanstalk has a lot of features, some of them being providing a way to configure your application environment, do tasks pre and post deployments, customizing AWS resources and much more.
Most of it is done through special folders that live in your code base, specifically `.ebextensions` and `.platform` (.platform is supported for Amazon Linux 2 (recommended) instances, for Amazon Linux 1, we use just ebextensions)

### What is HTTPS (A simplified version) ?

It is the secure version of HTTP which encrypts data that is transfered to increase secureity.  HTTPS not only encrypts the data but also helps the browser make sure that the data is going to the place it says it's going to. It identifies that when you send or recieve something from `google.com`, it goes and comes from `google.com`.

How all this is done is outside the scope of this article, but all you need to know is that this identification process requires a Certificate Authority to provide a "certificate" that is sent over and identifies your domain. We'll be using a well known and free certificate authority called let's encrypt. These certificate have exipiry dates and need renewal. Let's Encrypt provides a cli that can help us generate these programmatically.

### Setting up Nginx

Elastic beanstalk uses nginx as a default reverse proxy for your application, you can configure it and extend it by adding a `.conf` file to a folder name `.platform/nginx/conf.d` in your application source. These files are included automatically. A reverse proxy basically maps all incoming requests to suitable servers. You can learn a lot more about nginx on the web. It's a very large and intresting subject to read about.

```
~/workspace/my-app/
|-- .platform
|   -- nginx
|       -- conf.d
|           -- myconf.conf
|-- other source files
```

We'll be using this [source code from vahiwe](https://github.com/vahiwe/Elastic-Beanstalk-Single-Instance-SSL) and copy the `.platform` folders. The working of this is explained in this [awesome article by vahiwe](https://aws.plainenglish.io/setup-ssl-https-on-elastic-beanstalk-single-instance-environment-d748ea04437d).

### Installing Certbot

We use the `.ebextensions` folder from the same repo as above. It contains a `ssl.config` which is a EB config file and allows us to run some commands in the environment programmatically.
This file has the following `container_commands`

```
container_commands:
  10_downloadepel:
    command: "sudo wget -r --no-parent -A 'epel-release-*.rpm' https://dl.fedoraproject.org/pub/epel/7/x86_64/Packages/e/"
  20_installepel:
    command: "sudo rpm -Uvh dl.fedoraproject.org/pub/epel/7/x86_64/Packages/e/epel-release-*.rpm --force"
  30_enableepl:
    command: "sudo yum-config-manager --enable epel*"
  40_installcertbot:
    command: "sudo yum install -y certbot"
  50_getcert:
    command: "sudo certbot certonly --debug --non-interactive --email ${EMAIL_LINK} --agree-tos --standalone --domains ${DOMAIN_LINK} --keep-until-expiring --pre-hook \"sudo service nginx stop\" --post-hook \"sudo service nginx start\""
  60_link:
    command: "ln -sf /etc/letsencrypt/live/${DOMAIN_LINK} /etc/letsencrypt/live/ebcert"
```

This installs certbot and all it's dependencies in the AWS environment. It generates a SSL certificate using certbot for the first time using the environment variables `DOMAIN_LINK` and `EMAIL_LINK`, these are required variables and should be set from the EB console.

### Setting up autorenewal

The file also contains this piece of code that sets up a scheduled job or cron job that renews certbot weekly.

```
.... (stuff)
files:
  /etc/cron.d/certbot_renew:
    content: "@weekly root certbot renew\n"
    group: root
    mode: "000644"
    owner: root
.... (more stuff)
```

# Conclusion

And, there you have it, your application running on Elastic Beanstalk, with SSL security. You can just drag and drop a zip in Elastic Beantsalk Console for you environment and it'll deploy it.

**But what about CD?** Well, this article has become too long and has a lot of information. I'll be posting another short one soon with details about how to do CD.