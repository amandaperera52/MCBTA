
# DEPLOYING EC2 INSTANCE AND ESTABLISHING SSH SESSION CWL

Step 1: Configure the instance
Step 2: Choosing the appropriate instance type
Step 3 : Network configuration
Step 4: Launch Instance
Step 5: Take the ssh session

Step 1: Configure the instance

01 Configure EC2 instance

- Architecture -  64 bit
- OS - ubyntu
- Storage -  8

02 Make the SSH connection over the instance
- Copy the public ip of the instance
- Then ssh over the developed instance using below command

```
ssh -i "MCBTA SSH.pem" ubuntu@34.202.9.67
```

![imge](01.png)


# INSTALLING THE ELK : SIEM  CWL

Step 1: Configuring Elastic Repository over the base machine
Step 2: Install Elasticsearch over the instance
Step 3 : Configuring the elasticsearch.yml
Step 4: Testing the Deployed Elasticsearch Service

Step 1: Configuring Elastic Repository over the base machine
Before configuring Elastic/Kibana, it is recommended to set up the required repositories for the
installation

- Do the basic update using below command

```
 sudo apt-get update
```
img 02

- Deploying the required packages using below commands

```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg--dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
```

```
echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee/etc/apt/sources.list.d/elastic-8.x.list
```
By executing the above command, we will import the GPG key along with the necessary
packages and dependencies.

img 03

again update
```
 sudo apt-get update
```

Step 2: Install Elasticsearch over the instance
- Once the required packages are downloaded, we can proceed with installing Elasticsearch.
- Once the update is complete, proceed with installing Elasticsearch by running the command
below.

```
sudo apt install elasticsearch
```
img 04

In this step we have to make a note of credentials -  XPML-8RpDMTb1-Y70pzT

- Once the installation is successfully completed, we can enable the Elastic service and start
Elasticsearch

```
sudo systemctl enable elasticsearch.service
```
```
sudo systemctl start elasticsearch.service
```

img 05

Step 3 : Configuring the elasticsearch.yml

- After the service is successfully installed, we can proceed with modifying the configuration
located in the /etc/elasticsearch/elasticsearch.yml directory
```
sudo nano /etc/elasticsearch/elasticsearch.yml
```
img 06 

-In nano we can set these
network.host: 0.0.0.0
http.port: 9200

img 07

- Modifying the above-mentioned configuration allows global access to the Elastic service. If
needed, the port can also be adjusted according to the requirements. Once the configuration is
set, restart the service to apply the changes.
```
sudo systemctl restart elasticsearch.service
```
img 08







