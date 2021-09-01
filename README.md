# Instructions for setting up EC2 Machine
- In AWS, navigate to Services -> EC2 -> Launch instances
- Select the Ubuntu 16.04 LTS (HVM) machine
- Click Next: Configure Instance Details
- Click on the Subnet drop-down menu and select DevOpsStudent default 1a
- Click Next: Add Storage
- Click Next: Add Tags
- Click Add another tag
- Put 'Name' in the first input box, and 'SRE_Amy_app'
- Click Next: Configure Security Group
- Put 'sre_amy_app' into both the Security group name and the Description
- Click Add Rule and set the Type to SSH and the Source to My IP. Put 'access from my ip' into the Description
- Add another rule of Type: HTTP, with Source: Anywhere, and Description: 'public access'
- Click Review and Launch
- Click Launch
- In Git Bash, make sure you have a ~/.ssh folder and put the key file in there
- Back in AWS, select the relevant key pair
- Click Launch instances
- Response says "Your instances are now launching" with a link beside it; click the link
- Select the instance, then click Connect
- Click on the SSH Client tab
- In Git Bash, in the same folder as before, run the command given by Step 3 of the SSH Client tab, then run the line given in the example section of Step 4

**Your EC2 machine has just started up!**

- Run the following commands in the machine:
```bash
sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-get install nginx -y
sudo apt-get install python-software-properties -y
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install nodejs -y
sudo npm install pm2 -g -y
```
- Enter `exit`
- Run the following line in Git Bash to copy the app folder from my intro-to-cloud-computing folder to the EC2 machine:
```bash
scp -ri sre_key.pem ~/Documents/sreRepo/intro-to-cloud-computing/app/ ubuntu@34.240.158.131:/home/ubuntu/app
```
- To ssh back into the EC2 machine, enter the line from the example section of step 4 of the SSH Client tab (AWS)
- Enter the following command: `cd /home/ubuntu/app`
- Then `sudo npm install`
- Then `npm start`
- Navigate to the public IP address for the instance (to find this, go back to AWS and navigate to Instances -> your instance -> Details, and copy the Public IP address from there, then paste it into your browser)
- The nginx page should appear
- In AWS, in Instances -> your instance, click Security
- Click the name of the security group
- Add a rule of Type: Custom TCP, and set the Port range to 3000, the Source to Anywhere IPv4, and the Description to 'node app'
- Now add :3000 to the end of the instance's public IP address to view the test page