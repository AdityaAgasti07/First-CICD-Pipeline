#A simple jenkins pipeline to verify if the docker Agent configuration is working as expected.

Install Jenkins, configure Docker as agent, set up cicd, deploy applications to k8s and much more

# AWS EC2 Instance

![Screenshot 2024-03-20 000049](https://github.com/AdityaAgasti07/First-CICD-Pipeline/assets/159541012/46d5e7c1-7a25-4dfc-8697-accc3d634e54)

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

![Screenshot 2024-03-20 000025](https://github.com/AdityaAgasti07/First-CICD-Pipeline/assets/159541012/8e5c926c-03c4-45a0-a15f-45dac34b18f7)

## Click on Install Suggested Plugins

![Screenshot 2024-03-20 000327](https://github.com/AdityaAgasti07/First-CICD-Pipeline/assets/159541012/4978bdf7-6af3-4e0d-a7a0-50f73741e9c5)

Create First Admin User or Skip the step [If you want to use this Jenkins instance for future use-cases as well, better to create admin user]

![Screenshot 2024-03-20 000655](https://github.com/AdityaAgasti07/First-CICD-Pipeline/assets/159541012/742f8826-3126-4547-a3f1-b3dc06dd42a0)

Jenkins Installation is Successful. You can now starting using the Jenkins

![Screenshot 2024-03-20 000747](https://github.com/AdityaAgasti07/First-CICD-Pipeline/assets/159541012/b6c118de-ea5d-4f93-9668-3cc46072c59b)

## Install the Docker Pipeline plugin in Jenkins:

   - Log in to Jenkins.
   - Go to Manage Jenkins > Manage Plugins.
   - In the Available tab, search for "Docker Pipeline".
   - Select the plugin and click the Install button.
   - Restart Jenkins after the plugin is installed.

![Screenshot 2024-03-20 002712](https://github.com/AdityaAgasti07/First-CICD-Pipeline/assets/159541012/dca17f06-fcdf-44c5-8c34-14f9fe88ca16)

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
