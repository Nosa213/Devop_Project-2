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
    
    
Once plugins installation is done – create an admin user and you will get your Jenkins server address.

The installation is completed!
    
    
 <img width="1097" alt="Screenshot 2023-06-07 204037" src="https://github.com/Nosa213/Devop_Project-2/assets/125190958/8d6458c5-e00f-44ba-bde3-040d9dd53947">
    
    
    
Step 2 – Configure Jenkins to retrieve source codes from GitHub using Webhooks
In this part, you will learn how to configure a simple Jenkins job/project (these two terms can be used interchangeably). This job 
will will be triggered by GitHub webhooks and will execute a ‘build’ task to retrieve codes from GitHub and store it locally on 
Jenkins server.

1. Enable webhooks in your GitHub repository settings
    
  
    <img width="1121" alt="image" src="https://github.com/Nosa213/Devop_Project-2/assets/125190958/f4bc76f9-bf77-4146-9e73-28e5af21b4df">
    
    
    <img width="1141" alt="image" src="https://github.com/Nosa213/Devop_Project-2/assets/125190958/e489a4d2-dcfa-47b2-88a7-89aada728145">


 2. Go to Jenkins web console, click "New Item" and create a "Freestyle project" 
    
    
  <img width="1070" alt="image" src="https://github.com/Nosa213/Devop_Project-2/assets/125190958/8d9dad1e-aa25-4e25-8bac-82c9fa232cbf">

    
To connect your GitHub repository, you will need to provide its URL, you can copy from the repository itself
    
<img width="469" alt="image" src="https://github.com/Nosa213/Devop_Project-2/assets/125190958/db0da9a0-bc6f-4948-a80f-4e1e83841f0b">

 In configuration of your Jenkins freestyle project choose Git repository, provide there the link to your Tooling GitHub repository and credentials (user/password) so Jenkins could access files in the repository. 
   
 <img width="549" alt="image" src="https://github.com/Nosa213/Devop_Project-2/assets/125190958/0af891cb-236a-4fcd-8aed-a55d2d335104">
   
 Save the configuration and let us try to run the build. For now we can only do it manually. Click "Build Now" button, if you have configured everything correctly, the build will be successfull and you will see it under #1
    
<img width="1280" alt="Screenshot 2023-06-08 074949" src="https://github.com/Nosa213/Devop_Project-2/assets/125190958/d2cf7ce8-78ad-4561-a822-700ab4890b0e">


    
You can open the build and check in "Console Output" if it has run successfully.

If so – congratulations! You have just made your very first Jenkins build!

But this build does not produce anything and it runs only when we trigger it manually. Let us fix it.

Click "Configure" your job/project and add these two configurations Configure triggering the job from GitHub webhook:

    
 <img width="544" alt="image" src="https://github.com/Nosa213/Devop_Project-2/assets/125190958/107fae30-4a36-4859-a8e8-c4ede46ceef1">
   
     
    
Configure "Post-build Actions" to archive all the files – files resulted from a build are called "artifacts".
        
<img width="622" alt="Screenshot 2023-06-08 071318" src="https://github.com/Nosa213/Devop_Project-2/assets/125190958/08c44b90-ecee-4865-823e-c8d0ae3bf223">
    
   
Now, go ahead and make some change in any file in your GitHub repository (e.g. README.MD file) and push the changes to the master branch.

You will see that a new build has been launched automatically (by webhook) and you can see its results – artifacts, saved on Jenkins server.


 <img width="608" alt="image" src="https://github.com/Nosa213/Devop_Project-2/assets/125190958/1d484088-0c18-4cea-a638-b9be10f7a337">

    
    
You have now configured an automated Jenkins job that receives files from GitHub by webhook trigger (this method is considered as ‘push’ because the changes are being ‘pushed’ and files transfer is initiated by GitHub). There are also other methods: trigger one job (downstreadm) from another (upstream), poll GitHub periodically and others.

By default, the artifacts are stored on Jenkins server locally
    
```
ls /var/lib/jenkins/jobs/tooling_github/builds/<build_number>/archive/
```
 
# CONFIGURE JENKINS TO COPY FILES TO NFS SERVER VIA SSH

##  Step 3 – Configure Jenkins to copy files to NFS server via SSH
Now we have our artifacts saved locally on Jenkins server, the next step is to copy them to our NFS server to /mnt/apps directory.

Jenkins is a highly extendable application and there are 1400+ plugins available. We will need a plugin that is called "Publish Over 
SSH".

1. Install "Publish Over SSH" plugin.
On main dashboard select "Manage Jenkins" and choose "Manage Plugins" menu item.

On "Available" tab search for "Publish Over SSH" plugin and install it
    




  
