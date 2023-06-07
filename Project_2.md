# Continous-Integration-Pipeline-For-Tooling-Website

## DevOps Automation

Automation is the use of technology to perform tasks with reduced human assistance. Automation helps us accelerate processes and scale environments, as well as build continuous integration, continuous delivery, and continuous deployment (CI/CD) workflows. There are many kinds of automation, including IT automation, business automation, robotic process automation, industrial automation, artificial intelligence, machine learning, and deep learning.

Theoretically speaking, We could perform DevOps processes like Continuous Integration, Continuous Delivery and log analytics manually. But doing so would require a 
large team, a lot of time and a level of communication and coordination between team members that is just not realistic in most situations.

Automation makes it possible to perform these processes using software tools and preset configurations.


## Benefits of Automation in DevOps


We have seen earlier releases, in the absence of automation taking years to get into the production and also recently with agile, be it lean, scrum or safe, and with a percentage of automation being improved, release timelines are brought down to few months or weeks.But automation is absolutely a must in order to make the releases as fast as possible in a few hours. So, I think it is impossible to make such quick and frequent releases unless we put in automation in place throughout the pipeline.

So, quite obviously then, if we want to achieve the objectives of DevOps, high quality and value delivered to customers via frequent and fast deliveries, Automate everything is a must. Clearly, we know by now that automation removes manual errors, dependency on an individual, performs faster, and achieves accuracy thereby achieving consistency and reliability. Hence, automating everything enables the devops objective of high-quality delivery, enables frequent releases and faster
releases.



## In a nutshell, Automation,

- Removes manual errors
- Team members are empowered
- Dependency removed
- Latency removed
- Increases no of deliveries
- Reduces the lead time
- Increases frequency of releases
- Provides faster feedback
- Enables speed, reliability, and consistency.



![image](https://user-images.githubusercontent.com/85270361/168469493-6d91c256-226e-4e20-911a-38f04238752d.png)


## Acording to Circle CI, Continuous integration (CI) is a software development strategy that increases the speed of development while ensuring the quality of the 
code that teams deploy. Developers continually commit code in small increments (at least daily, or even several times a day), which is then automatically built 
and tested before it is merged with the shared repository.



# In this project, We are required to implement CI for Tooling Website using Jenkins.


Below is the updated architecture of our infrastructure. Jenkins will be used for continous integration, and its data will be stored on a remote NFS server.



![image](https://user-images.githubusercontent.com/85270361/168469571-4918b224-1933-46f0-9c13-9f7f0d89379b.png)


# INSTALL AND CONFIGURE JENKINS SERVER

Step 1 – Install Jenkins server

1. Create an AWS EC2 server based on Ubuntu Server 20.04 LTS and name it "Jenkins"

2. Install JDK (since Jenkins is a Java-based application)

```
sudo apt update
sudo apt install default-jdk-headless
```

3. Install Jenkins

```
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
    /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt-get install jenkins
```

Make sure Jenkins is up and running

```
sudo systemctl status jenkins
```

4. By default Jenkins server uses TCP port 8080 – open it by creating a new Inbound Rule in your EC2 Security Group


<img width="1049" alt="image" src="https://github.com/Nosa213/Devop_Project-2/assets/125190958/10eff18c-5257-44d9-9fb8-d068245b73ab">



5. Perform initial Jenkins setup.
From your browser access http://<Jenkins-Server-Public-IP-Address-or-Public-DNS-Name>:8080

You will be prompted to provide a default admin password


<img width="1070" alt="Screenshot 2023-06-07 201622" src="https://github.com/Nosa213/Devop_Project-2/assets/125190958/26bf9d9d-8631-4b8e-b267-95ac9c77ce49">



  
  Retrieve it from your server:
  
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
  
Then you will be asked which plugings to install – choose suggested plugins.
  
  
  <img width="856" alt="image" src="https://github.com/Nosa213/Devop_Project-2/assets/125190958/613fcf76-dc91-4930-a16f-45f6f65b5f2c">

  
