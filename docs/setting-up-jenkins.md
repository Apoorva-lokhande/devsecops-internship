# Setting up Jenkins 

## Objective

This section aims to set up the required infrastructure of Jenkins to perform the task and solve the 2nd point of the [Problem Statement](https://devsecops-report.netlify.app/problem-statements/).
## What is Jenkins? 

Jenkins is a self-contained, open-source automation server that can be used to automate all sorts of tasks related to building, testing, and delivering or deploying software.  

## Installation steps for Jenkins  

### Prerequisite 

- I have set up the `ubuntu 18.04` VM, installing Jenkins from [Documentation](https://www.jenkins.io/doc/book/installing/). 

- I have installed `java 8 OpenJDK` and `JRE (Java Development Kit and Java Runtime Environment)` which is used to develop and run the software, I have used this [Link](https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-18-04#installing-specific-versions-of-openjdk) to download the same.
Add the repository key to the terminal:  

    wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add - 

![image](pictures/jenk.png) 

The system will return `OK`  

Next, add the Debian package repository address:   

    sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \ 
    /etc/apt/sources.list.d/jenkins.list 

    sudo apt update 

![image](pictures/last.png) 

Now install Jenkins and its dependencies: 

    sudo apt install jenkins  

![image](pictures/installed.png) 

### Starting Jenkins 

The systemctl command is used to manage `systemd` services and service manager:  

    sudo systemctl start jenkins 

Check the status of Jenkins service using the below command:  

    sudo systemctl status jenkins 

And the Jenkins has been installed successfully, the output is showing as Active: **active(excited)**. To reach it from a web browser I will adjust the firewall rules to complete the initial setup.
![image](pictures/startandstatus.png)   

### Set-up a Firewall with UFW 

A firewall is a software controlling incoming and outgoing network traffic. A firewall can manage traffic by monitoring network ports. 

By default, Jenkins runs on port 8080. And opening the using ufw(uncomplicated firewall): 

    sudo ufw allow 8080 

To check the status of the ufw: 

    sudo ufw status 

![image](pictures/activee.png) 

If the status shows "Inactive". Then enable using the following command :

    sudo ufw enable 

To configure your server to allow incoming SSH connections, you can use this command: 

    sudo ufw allow ssh    

### Setting up Jenkins 

To find your server's IP address or domain name enter the following command in your terminal: 

    ifconfig  

Using the server's name or domain name as shown in the following command, entering that into the browser, in turn, gave the `Unlock Jenkins` window. 

http://your_server_name_or_domain:8080 

### Unlock Jenkins 
The Unlock Jenkins window shows where the admin password is stored. In the terminal I will use the cat command to display the password: 
 
    sudo cat /var/lib/jenkins/secrets/initialAdminPassword 

The 32-character alphanumeric password is displayed in the terminal, paste it onto the Administrator password field, and then click on `continue`. 
![image](/pictures/unlock.png) 
 

#### Customize Jenkins  

In the Customize Jenkins select `install suggested plugins` which will start the installation process directly and click on `continue`.
![image](/pictures/costumize.png) 

#### Create Admin User  

Add the required credentials, click on `save` and continue as admin. 

The `Instance configuration` page will be displayed which will ask to confirm the preferred URL for Jenkins instance, click on `save` and `finish`.  
![image](/pictures/info.png) 


#### Installation Starts 
Once the process is over click on `Reboot` which will restart the Jenkins.
![image](/pictures/started.png) 

Now the Jenkins is running Successfully, now typing the below command become the Jenkins user:

    sudo su - jenkins




 
 
 

 