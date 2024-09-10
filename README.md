# aws-ECR-jenkins
a project building and pushing aof docker images into another repository using AWS-ECR using jenkins pipeline
Step #1:Configuring EC2 instance in AWS
3.0 Go to the AWS dashboard and then to the EC2 services. create an instance
Step #2:Install Java on Ubuntu 22.04 LTS
After the successful SSH connection, firstly update the Linux machine. And install java using below commands:

sudo apt update
Now lets install java 17

sudo apt install openjdk-17-jre
Lets check the version of java

java -version

Step #3:Install Jenkins on Ubuntu 22.04 LTS
Lets install jenkins using below commands

curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
 /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
Step #4:Enable and start Jenkins on Ubuntu 22.04 LTS
You can enable the Jenkins service to start at boot with the command

sudo systemctl enable jenkins
You can start the Jenkins service with the command

sudo systemctl start jenkins
You can check the status of the Jenkins service using the command

sudo systemctl status jenkins


Step #4:Install git on Ubuntu 22.04 LTS
We need to Install git using below command

sudo apt install git

Step #5:Install Docker on Ubuntu 22.04 LTS
Now here we need to Install Docker

sudo apt  install docker.io
After Installing Docker we need to give some permission

sudo usermod -aG docker $USER
sudo chmod 666 /var/run/docker.sock
After installing docker lets Restart jenkins

sudo systemclt restart jenkins


Step #6:Access Jenkins on Browser
https//:<Instance_ip>:8080
After that On the browser, you should see the Jenkins interface that asks for the administrator password.
Now cat the following Jenkins file to retrieve the Administrator password and paste it to the Jenkins dashboard.

Here, create a Jenkins user

After the configuration is completed, you should see the Jenkins dashboard.


Step #7:Add AWS credentials in Jenkins
We may also set up AWS credentials in Jenkins so that it facilitates the Docker push to the ECR repository.

GO to the Manage Jenkins>>Credentials>>system>>Global credentials


Then add credentials and here add AWS username and password and account ID

Step #8:Installing plugins in Jenkins
Go to the manage Jenkins>>Plugins>>Available Plugin

Docker
Docker Pipeline
Amazon ECR plugin

Step #9:Creating ECR Repository in AWS
Lets Create AWS ECR repository to push this image so Go to AWS ECR repository and create

Step #10:Create AmazonEC2ContainerRegistryFullAccess IAM Role in AWS
Here in this step we need to create IAM role with below permission 

Attach permission policies : AmazonEC2ContainerRegistryFullAccess

Step #11:Install AWS CLI on Ubuntu 22.04 LTS
You can go to the official site of AWS and Install

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip 
sudo ./aws/install

Step #12:Push Docker image to AWS ECR using Jenkins pipeline
So lets create jenkins pipeline go to the Jenkins Dashboard Click on new Item select Pipeline and paste the code on the jenkinsfile






