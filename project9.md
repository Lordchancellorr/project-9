## Documentation of Project 9

- TOOLING WEBSITE DEPLOYMENT AUTOMATION WITH CONTINUOUS INTEGRATION. INTRODUCTION TO JENKINS
[Jenkins](https://en.wikipedia.org/wiki/Jenkins_software) is a free and open source automation server It is one of the mostl popular Continuous Integration/Continuous Delivery tools, it was created by a former Sun Microsystems developer Kohsuke Kawaguchi and the project originally had a named "Hudson". In this project, I utilized Jenkins' continuous integration capabilities to make sure that all the changes i  made to the source code in ny Github Tooling repository will immediately be updated to the Tooling website which was created in [project 7](https://github.com/Lordchancellorr/project-7) and updated in [Project 8](https://github.com/Lordchancellorr/project-8)

[Jenkins](https://en.wikipedia.org/wiki/Jenkins_software) is an open source automation server. It helps automate the parts of software development related to building, testing, and deploying, facilitating continuous integration and continuous delivery. It is a server-based system that runs in servlet containers such as Apache Tomcat. It supports version control tools, including AccuRev, CVS, Subversion, Git, Mercurial, Perforce, ClearCase and RTC, and can execute Apache Ant, Apache Maven and sbt based projects as well as arbitrary shell scripts and Windows batch commands-[(read more)](https://www.jenkins.io/). Now we will swiftly proceed to the implementation of the project.

- INSTALLATION AND CONFIGURURATION OF JENKINS SERVER
A new ec2 server of Ubuntu 20.02 verison was spinned up, made it TCP port 8080(Inbound security rule), and after a successful connection and update, I ran the following commands-`sudo apt install default-jdk-headless`, `wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key` | `sudo apt-key add -`
`sudo sh -c echo deb https://pkg.jenkins.io/debian-stable binary/ > \ /etc/apt/sources.list.d/jenkins.list`
`sudo apt update` `sudo apt-get install jenkins`   To confirm the status of jenkins, `sudo systemctl status jenkins` and it was active and running- check the image below: ![Jenkins status]()
i accesed the paage with jenkins server IP address, retrieved the password with `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`  as instructed in the documentation and the images below were the output after a successful login.
- ![Jenkins Login Page]()
- [Jenkins Installation]()
- ![Jenkins Dashboard]()
-After all these, i moved to the configuration in other to retreive source codes from GitHub using Webhooks, i forked the tooling repo directly from darey.io Github account to my own repositories. I opened the already installed jenkins, created a new console, followed all the instructions in the documentation. The images below are proof of successful configuration.

![Confirmation of push request]()

![Artifacts]()

![Confirmation of Artifacts]()

I was able to configure an automated Jenkins job that receives files from GitHub by webhook trigger (this method is considered as ‘push’ because the changes are being ‘pushed’ and files transfer is initiated by GitHub.

CONFIGURATION OF  JENKINS TO COPY FILES TO NFS SERVER VIA SSH
Inside the Jenkins main dashbord, 'Manage Jenkins, i downloaded the 'published over SSH which automatically saved on my account.
I configured the job/project to copy artifacts over to NFS server and on the main dashboard, I selected  "Manage Jenkins" and choose "Configure System" menu item.

Scrolled down to Publish over SSH plugin configuration section and configure it to be able to connect to your NFS server:

Provided a private key 
Hostname was the  private IP address of your NFS server
Username was ec2-user (since NFS server is based on EC2 with RHEL 8)
Remote directory – /mnt/apps since our Web Servers used it as a mointing point to retrieve files from the NFS server
After following the documentation to the latter, the images below were the outputs.
![Successful Configuration]() ------(First attempt)
![Successful Configuration](second attempt)

to confirm the workabilty and reliace on the configuration and connection built for jenkins on github and NFS and the image below was the output on the terminal after i ran `cat /mnt/apps/README.md`

![Jenkins Configuration]()

This brings us to the end of Project 9
Thank you!












