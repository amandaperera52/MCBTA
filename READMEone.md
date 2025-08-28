
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

Step 4: Testing the Deployed Elasticsearch Service

- Once all the required installations and configurations are complete, validate the setup by either running the command below or accessing the service using the configured IP and port.

```
sudo systemctl status elasticsearch.service
```
img 09

- Then go to AWS and set network rules
  security > security group > inbound rule / outbound rule
  Here we can add rules what are the ports we want to access VM.
  ex -: add elastic port - 9200, kibana port - 5601
  
- Then we can try login to the elastic using username and password
  https://(public ip of instance):9200

img 16 

Successfully configures elastic search and start


# DEPLOYING AND CONFIGURING 
THE KIBANA SERVICE 
Step 1: Installing the kibana service 
Step 2: Configuring the kibana.yml
Step 3 : Starting the kibana service
Step 4: Validate the Deployed Kibana Service


Step 1: Installing the kibana service

- Update
```
 sudo apt-get update
```

- The next step is to configure and install the Kibana service. Since the required packages have
already been set up, we can proceed directly with the installation by running the command
below

```
sudo apt install kibana
```
img 10

- Once the installation is successfully completed, we can enable the Kibana service and start
Kibana

```
sudo systemctl enable kibana.service
```
```
sudo systemctl start kibana.service
```
img 11

Step 2: Configuring the kibana.yml
- Once configured, proceed to modify the settings in the /etc/kibana/kibana.yml file
```
sudo nano /etc/kibana/kibana.yml
```
img 12

- we can change server port and server host
  img 13
  
- Modifying the above-mentioned configuration allows global access to the Kibana service. If
needed, the port can be adjusted according to your requirements. Once the configuration is set,
restart the service to apply the changes.

```
sudo systemctl restart kibana.service
```
img 14

Step 3: Starting the kibana service
- Once all the required installations and configurations are complete, enable the Kibana service
and start it.
```
sudo systemctl enable kibana
```
```
sudo systemctl start kibana
```
Step 4: Validate the Deployed Kibana Service
- After completing all the required installations and configurations, validate the setup by either
running the command below or accessing the service using the configured IP and port

- Check the status of the servers
```
sudo systemctl status kibana.service
```
img 15

Kibana has been Successfully deployed and servers has configured.

img 17



