For this week Assignment we are setting up the honeypot by signup google cloud platform and set up mhn sever using ubuntu 14.04.
Two major firewall rules for creating the instance
HTTP traffic allowed (port 80)
  If you are create VM instance through google cloud platform then check the http allow traffic
  ELSE
    >gcloud compute firewall-rules create NAME_OF_YOUR_INSTANCE --allow tcp:80

TCP ports 3000 and 10000 need to be open to allow incoming (aka 'ingress') traffic



