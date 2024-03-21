#A simple jenkins pipeline to verify if the docker Agent configuration is working as expected.

Install Jenkins, configure Docker as agent, set up cicd, deploy applications to k8s and much more

# AWS EC2 Instance

 ![Screenshot 2024-03-20 000049](https://github.com/AdityaAgasti07/My-first-Pipeline/assets/159541012/d77b339f-b506-4f4b-ad52-f0fb929db9ff)

# Install Jenkins 
install java

```bash
sudo apt update
sudo apt install openjdk-11-jre
```
Verify Java is installed
```bash
java --version
```
Now you can proceed with installing jenkins

```bash
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

## Login to Jenkins using the below URL:

http://:8080 [You can get the ec2-instance-public-ip-address from your AWS EC2 console page]

Note: If you are not interested in allowing All Traffic to your EC2 instance 1. Delete the inbound traffic rule for your instance 2. Edit the inbound traffic rule to only allow custom TCP port 8080

After you login to Jenkins, - Run the command to copy the Jenkins Admin Password - sudo cat /var/lib/jenkins/secrets/initialAdminPassword - Enter the Administrator password

![Screenshot 2024-03-20 000025](https://github.com/AdityaAgasti07/My-first-Pipeline/assets/159541012/c2143db1-c527-4916-88a8-ccef3377a43d)

## Click on Install Suggested Plugins

![Screenshot 2024-03-20 000327](https://github.com/AdityaAgasti07/My-first-Pipeline/assets/159541012/15b2835f-0b50-40ed-93d0-72c62ee25276)

Create First Admin User or Skip the step [If you want to use this Jenkins instance for future use-cases as well, better to create admin user]

![Screenshot 2024-03-20 000655](https://github.com/AdityaAgasti07/My-first-Pipeline/assets/159541012/ebbda002-8b0f-4add-94b1-ebbabb475af4)

Jenkins Installation is Successful. You can now starting using the Jenkins

![Screenshot 2024-03-20 000747](https://github.com/AdityaAgasti07/My-first-Pipeline/assets/159541012/ba97709a-65b1-49b8-8886-2e53377bd2dd)

## Install the Docker Pipeline plugin in Jenkins:

   - Log in to Jenkins.
   - Go to Manage Jenkins > Manage Plugins.
   - In the Available tab, search for "Docker Pipeline".
   - Select the plugin and click the Install button.
   - Restart Jenkins after the plugin is installed.

![Screenshot 2024-03-20 002712](https://github.com/AdityaAgasti07/My-first-Pipeline/assets/159541012/377d54ec-4286-4e8d-9409-8b2a06df917b)

Wait for the Jenkins to be restarted.


## Docker Slave Configuration

Run the below command to Install Docker

```
sudo apt update
sudo apt install docker.io
```
 
### Grant Jenkins user and Ubuntu user permission to docker deamon.

```
sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
```

Once you are done with the above steps, it is better to restart Jenkins.

```
http://<ec2-instance-public-ip>:8080/restart
```

The docker agent configuration is now successful.
