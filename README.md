# Deploying a Web Application using AWS Code Deploy

1: On you EC2 Instance install the below aws code deploy agent.

    1.) When server is booted run the following commands as root.

        yum -y update

        yum install -y aws-cli

        cd /home/ec2-user

    2.) Here you will setup your AWS access, secret, and region.

        aws configure

        wget https://aws-codedeploy-ap-southeast-1.s3.amazonaws.com/latest/install

        chmod +x ./install

    3.) This is simply a quick hack to get the agent running faster.

        sed -i "s/sleep(.*)/sleep(10)/" install

        ./install auto

    4.) Verify it is running.

        service codedeploy-agent status
 
2: On another EC2 Instance Install Jenkins as below:
    
    1. ) wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo
    2. ) rpm --import http://pkg.jenkins-ci.org/redhat-stable/jenkins-ci.org.key
    3. ) yum install jenkins
    4. ) yum install git
    5. ) service jenkins start
    6. ) chkconfig jenkins on (to start jenkins whenever the server restarts)
    7. ) Navigate to http://<EC2 PUBLIC IP>:8080
    8. ) Under Manage Plugins Install AWS Code Deploy Plugin and GIT as shown in the below fig.
   ![Upload_Pic](https://github.com/maheshshekhar/deploy/blob/master/git.png)
   ![Upload_Pic](https://github.com/maheshshekhar/deploy/blob/master/awscd.png)
  
3: In you github add the webhook to the Jenkins EC2 Server.
   ![Upload_Pic](https://github.com/maheshshekhar/deploy/blob/master/github.png)
 
4: On you AWS Console create an AWS Code Deploy Application
   
    1. ) Provide the Application Name, Deployment Group, The instance on which the application should run.

5: We have an appsec.yml file which will provides the details to the server. It provides the list of application needs to be installed using the scripts

