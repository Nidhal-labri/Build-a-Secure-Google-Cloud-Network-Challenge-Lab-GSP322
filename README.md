# Build-a-Secure-Google-Cloud-Network-Challenge-Lab-GSP322
## ***```Build a Secure Google Cloud Network: Challenge Lab GSP322```***

### Export all the values carefully

```bash
export SSH_IAP_NETWORK_TAG=

export SSH_INTERNAL_NETWORK_TAG=

export HTTP_NETWORK_TAG=

export ZONE=
```
###
###


### ***NOW JUST COPY THE CODE AND PASTE ON YOUR CLOUD SHELL***
###
###

```bash

gcloud compute firewall-rules delete open-access --quiet

gcloud compute instances start bastion --zone=$ZONE --quiet

gcloud compute firewall-rules create ssh-ingress --allow=tcp:22 --source-ranges 35.235.240.0/20 --target-tags $SSH_IAP_NETWORK_TAG --network acme-vpc --quiet

gcloud compute instances add-tags bastion --tags=$SSH_IAP_NETWORK_TAG --zone=$ZONE --quiet

gcloud compute firewall-rules create allow-http --allow tcp:80 --source-ranges 0.0.0.0/0 --target-tags=$HTTP_NETWORK_TAG --network=acme-vpc --quiet

gcloud compute instances add-tags juice-shop --tags=$HTTP_NETWORK_TAG --zone=$ZONE --quiet

gcloud compute firewall-rules create internal-ssh-ingress --allow tcp:22 --source-ranges=192.168.10.0/24 --target-tags=$SSH_INTERNAL_NETWORK_TAG --network=acme-vpc --quiet

gcloud compute instances add-tags juice-shop --tags=$SSH_INTERNAL_NETWORK_TAG --zone=$ZONE --quiet

```

#In Compute Engine -> VM Instances page, click the SSH button for the bastion host. Then SSH to juice-shop by <span style="color:red">red colored text</span>.



```bash

ssh 192.168.11.2 #Internal IP address of juice-shop

```

### Then Congratulations !!!
