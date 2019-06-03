# Project Title : Linux_Server_Configuration
This is the final project for "Full Stack Web Developer Nanodegree" on Udacity.
A Linux virtual machine (Amazon Lightsail / Ubuntu) is configured for Item Catalog application website.
You can visit the web site at : http://3.217.93.239/
* Public Static IP Address: 3.217.93.239
* SSH Port: 2200
* HTTP Port: 80
* NTP Port: 123

## Environment Used

This page explains how to secure and set up a Linux distribution on a virtual machine, install and configure a web and database server to host a web application..
* The Linux distribution is Ubuntu 16.04 LTS.
* The virtual private server is [Amazon Lighsail](https://aws.amazon.com/lightsail/).
* The web application is my [Item Catalog ](https://github.com/arbidha/Item_Catalog)project created earlier in this Nanodegree program.
* The database server is PostgreSQL.
* Local machine Windows 10

## Get a Server 


### Step 1: Start a new Ubuntu Linux server instance on Amazon Lightsail 

- Login into [Amazon Lightsail](https://lightsail.aws.amazon.com/ls/webapp/home/resources) using an Amazon Web Services account.
- Once you are login into the site, click `Create instance`. 
- Choose `Linux/Unix` platform, `OS Only` and  `Ubuntu 16.04 LTS`.
- Choose a instance plan (I took the cheapest, $3/month).
- Keep the default name provided by AWS or rename your instance.
- Click the `Create` button to create the instance.
- Wait for the instance to start up.
#### Create Static IP Address
- Inside the instance dashboard .
- On the Lightsail home page, choose Networking.
- Choose Create static IP.
- Select the AWS Region where you want to create your static IP.
- Choose the Lightsail resource (Catalog-Item)
- Name your static IP, and then choose Create.

**Reference**
- ServerPilot, [How to Create a Server on Amazon Lightsail](https://serverpilot.io/community/articles/how-to-create-a-server-on-amazon-lightsail.html).
- [Create a static IP and attach it to an instance in Amazon Lightsail](https://lightsail.aws.amazon.com/ls/docs/en_us/articles/lightsail-create-static-ip).


### Step 2: SSH into the server

- From the `Account` menu on Amazon Lightsail, click on `SSH keys` tab and download the Default Private Key.
- Move this private key file named `LightsailDefaultPrivateKey-*.pem` into the local folder `~/.ssh` and rename it `Catalog-Item.pem`.
- In your terminal, type: `chmod 644 ~/.ssh/Catalog-Item.pem`.
- To connect to the instance via the terminal: ` ssh ubuntu@3.217.93.239 -i ~/.ssh/Catalog-Item.pem`, 
  where `3.217.93.239` is the public static IP address of the instance.

<!--
Public IP address is 3.217.93.239.
ssh ubuntu@3.217.93.239 -i ~/.ssh/Catalog-Item.pem
-->
## Secure the server

### Step 3: Update and upgrade installed packages

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get autoremove
```


### Step 4: Change the SSH port from 22 to 2200

- Edit the `/etc/ssh/sshd_config` file: 
    `sudo nano /etc/ssh/sshd_config`.
- Then change the following 
  - Add Port 2200 below Port 22 (don't delete port 22 until 2200 is working) write file and exit (ctrl o, enter, ctrl x)
  - Find PermitRootLogin and edit to no.
  - Find the PasswordAuthentication line and edit it to no
  - Restart SSH: 
      `sudo service ssh restart`.

### Step 5: Configure the Uncomplicated Firewall (UFW)

- Configure the default firewall for Ubuntu to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123).
  ```
  sudo ufw status                  # The UFW should be inactive.
  sudo ufw default deny incoming   # Deny any incoming traffic.
  sudo ufw default allow outgoing  # Enable outgoing traffic.
  sudo ufw allow 2200/tcp          # Allow incoming tcp packets on port 2200.
  sudo ufw allow www               # Allow HTTP traffic in.
  sudo ufw allow 123/udp           # Allow incoming udp packets on port 123.
  sudo ufw deny 22                 # Deny tcp and udp packets on port 53.
  ```

- Turn UFW on: `sudo ufw enable`. The output should be like this:
  ```
  Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
  Firewall is active and enabled on system startup
  ```

- Check the status of UFW to list current roles: `sudo ufw status`. The output should be like this:

  ```
  Status: active
  
  To                         Action      From
  --                         ------      ----
  2200/tcp                   ALLOW       Anywhere                  
  80/tcp                     ALLOW       Anywhere                  
  123/udp                    ALLOW       Anywhere                  
  22                         DENY        Anywhere                  
  2200/tcp (v6)              ALLOW       Anywhere (v6)             
  80/tcp (v6)                ALLOW       Anywhere (v6)             
  123/udp (v6)               ALLOW       Anywhere (v6)             
  22 (v6)                    DENY        Anywhere (v6)
  ```

- Exit the SSH connection: `exit`.

- Click on the `Manage` option of the Amazon Lightsail Instance, 
then the `Networking` tab, and then change the firewall configuration to match the internal firewall settings above.
  <img src="images/screen4.png" width="600px">

- Allow ports 80(TCP), 123(UDP), and 2200(TCP), and deny the default port 22.
  <img src="images/screen5.png" width="600px">

- From your local terminal, run: `ssh -i ~/.ssh/lightsail_key.rsa -p 2200 ubuntu@13.59.39.163`, where `13.59.39.163` is the public IP address of the instance.

<!--
Public IP address is 13.59.39.163.
ssh -i ~/.ssh/lightsail_key.rsa -p 2200 ubuntu@13.59.39.163
-->

**References**
- Official Ubuntu Documentation, [UFW - Uncomplicated Firewall](https://help.ubuntu.com/community/UFW).
- TechRepublic, [How to install and use Uncomplicated Firewall in Ubuntu](https://www.techrepublic.com/article/how-to-install-and-use-uncomplicated-firewall-in-ubuntu/).



## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc
