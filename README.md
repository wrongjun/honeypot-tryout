For this week Assignment we are setting up the honeypot by signup google cloud platform and set up mhn sever using ubuntu 14.04.


## Create VM instance and setup fire wall

Two major firewall rules for creating the instance

HTTP traffic allowed (port 80)

  If you are create VM instance through google cloud platform then check the http allow traffic
  
  ELSE
  
    >gcloud compute firewall-rules create NAME_OF_YOUR_INSTANCE --allow tcp:80


TCP ports 3000 and 10000 need to be open to allow incoming (aka 'ingress') traffic

  >gcloud beta compute firewall-rules create mhn-allow-admin --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:3000,tcp:10000 --source-ranges=0.0.0.0/0 --target-tags=mhn-admin

Create VM instance 

>gcloud compute instances create "mhn-admin" --machine-type "f1-micro" --subnet "default" --maintenance-policy "MIGRATE"  --scopes "https://www.googleapis.com/auth/devstorage.read_only","https://www.googleapis.com/auth/logging.write","https://www.googleapis.com/auth/monitoring.write","https://www.googleapis.com/auth/servicecontrol","https://www.googleapis.com/auth/service.management.readonly","https://www.googleapis.com/auth/trace.append" --tags "mhn-admin","http-server","https-server" --image "ubuntu-1404-trusty-v20171010" --image-project "ubuntu-os-cloud" --boot-disk-size "10" --boot-disk-type "pd-standard" --boot-disk-device-name "mhn-admin"

## Setup up MHN(Modern Honey Network) sever
[The setup is under the instruction of MHN sever.](https://github.com/threatstream/mhn#installing-server-tested-ubuntu-12043-x86_64-and-centos-67)

This step will be take 40 mins to finish.


## deploy honey pot

Create another vm instance that can de delop the honeypot.

Login in to the mhn console with your username and password that you enter for the creation of the mhn sever. Following into the deloy in the navigation bar. Check out the scriptes, there will be several honey pots that can be deploy. Copy the delop comment and run in the new vm instance console.

>wget ......
I have deloy two honey pot. One is Ubuntu 14.04/Centos 7 - Dionaea and the other one is Ubuntu - Dionaea with HTTP.

## Summery of the honey pot attacts

Once i deloy the honey pot, there is a attack come in. 

I had been deloy two honeypots around three hours. All the attack had been save in [session.json](https://github.com/wrongjun/honeypot-tryout/blob/master/session.json).

In the first hour, Most of attack are from this three sites.

  1.144.202.81.254 (25 attacks)
  
  2.138.68.229.208 (20 attacks)
  
  3.104.248.6.137 (17 attacks)
  
After a hour, two IP form the most attacks.

  1.62.210.141.119 (40 attacks)
  
  2.122.114.180.183 (32 attacks)
  
  
TOP 5 Attacked ports:

  1.8088 (236 times)
  
  2.5060 (44 times)
  
  3.23 (37 times)
  
  4.3306 (32 times)
  
  5.445 (17 times)


## Resources
-MHN Sever(https://github.com/threatstream/mhn#installing-server-tested-ubuntu-12043-x86_64-and-centos-67)







