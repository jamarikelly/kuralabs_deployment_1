# Documentation for Second Deployment 

## Set Up

1. Login to aws console and start an ec2 ubuntu instance with security groups 22, 80 and 8080. 

2. Remote into the ec2 using virtual machine and use the commands below to install jenkins and start jenkins.
```
sudo apt update && upgrade
sudo apt install default-jre
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins

```
3. To configure jenkins; follow instructions below:
- connect to http://<your_server_public_DNS>:8080 from your browser; the jenkins management interface will come up. 
- Enter the command below to be able to set up jenkins.
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
- After you will be prompted to create a new admin user, enter your credentials.
- After user is created, go to manage plugins and select the available tab, add amazon Ec2 plugin, then install without restart.
- Once installation is finished, go back to the dashboard and select configure a cloud.
- Select add a new cloud and select amazon Ec2. A collection of fields appears.
- after, go back to the amazon console and terminate the instance. 



4. To install the Virtual Environment on your EC2 enter commands below
```
sudo apt install python3-pip
sudo apt install python3-10-venv
```
5. Connecting Github to Jenkins Server

- Fork the deployment repo firstly. https://github.com/kura-labs-org/kuralabs_deployment_1.git
- Create access token from github by navigating to github settings, select developer settings.
- select personal access token and create a new token; select "Repo" and "admin:repo_hook" for the token's permissions 

- Log back into the jenkins and select "New Item"
- Select multibranch pipeline
- Enter a display name and brief description of what youre doing 
- Add a branch source by selecting add source and select github
- Select the add button and select Github
- Click on add and then select jenkins 
- Under the username, enter your github username 
- Under password, enter the token copied from github
- Enter your url to the repository and you can validate by selecting validate.
- After its validated, click apply then save.
- You should see the build happening, if not, scan the repository.

6.
