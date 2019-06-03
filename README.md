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
* The virtual private server is Amazon Lighsail.
* The web application is my Item Catalog project created earlier in this Nanodegree program.
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
Public IP address is 13.59.39.163.
ssh -i ~/.ssh/lightsail_key.rsa ubuntu@13.59.39.163
-->

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
