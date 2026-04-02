## Jenkins Free Style Deployment 



Task: Deploy Application to Application Server (Tomcat) using Jenkins FreeStyle

Tools Used:

    GIT → Source Code Management Tool

    Maven → Building Tool

    Jenkins → CI Server

    Tomcat → App Server


Process:

Launch 2 Instances, Jenkins & Tomcat

Amazon Linux, Kernel 5.10, t2.micro

Enable 8080 in security group inbound rule otherwise both won’t work

Do Jenkins Setup 1st, Create a Job and get the code from Github repo using SCM

Install maven in Jenkins Server
 

	“yum install maven -y”

Go to Jenkins Dashboard → Configure the Job

Go to Build Steps → Choose “Invoke top-level maven targets”

Use code: 

    “clean package”

Save and Run the Build

Check Workspace for Build file


2. Set Up Tomcat server

Connect Tomcat server using command prompt

Install Dependency first

    “yum install java-17-amazon-corretto -y”

Download Tomcat file from dlcdn.apache.org using wget

Untar the file

Go to file → bin → sh startup.sh

Access the tomcat server using publicip:8080 

Go to manager App

By default, Access will be denied for us

Go to Tomcat Server

Go to tomcat directory and go to

    cd /webapps/manager/META-INF

Vim context.xml
Delete 2 lines from line no.22 starts from <value

Go to cd /apache-file/conf/

        vim tomcat-user.xml and add below content after last line

    <role rolename = “manager-gui”/>
    <role rolename = “manager-script/>


    <user username=”tomcat” password=”admin123” roles=”manager-gui”,manager-script/>



Restart the Tomcat Server

	Sh shutdown.sh
	Sh startup.sh

That’s It, Tomcat Setup is Done!!!
It’s time to Deploy

Go to Jenkins Dashboard

Go to Manage Jenkins

Go to Plugins

Install “Deploy to container” plugin

Go to Jenkins Job

Configure
Go to “Post-Build Actions” and Click Select “Deploy war/ear to container”

Give path as war file path “target/*.war”

Context → Give any name Ex: Swiggy

Select Container as tomcat 9.x remote

Give Tomcat Credentials

Give Tomcat URL

Save & Build

If Build Success, Refresh Tomcat Manager App to see Swiggy app, You can access that application by clicking on it


Jenkins FREE STYLE Deployment is Done!!!
