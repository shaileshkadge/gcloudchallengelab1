# gcloudchallengelab1
Getting Started Create and Manage Cloud Resourses: Challenge Lab |  Google cloud shell commands

OPEN CLOUD SHELL AND PASTE THE BELOW COMMANDS 
---------------------------------------------------------------------------------------------------------------------


gcloud compute project-info describe --project  (COPY AND PASTE YOUR PROJECT ID HERE and use this whole command)   


export PROJECT_ID=(PUT YOUR PROJECT ID HERE)
export ZONE= us-east1-b
echo $PROJECT_ID
echo $ZONE


gcloud compute instances create nucleus-jumphost --machine-type f1-micro --zone $ZONE


------------------**CHECK YOUR FIRST PROGRESS NOW**------------------------------------------------------------------ 


gcloud config set compute/zone us-east1-b
gcloud container clusters create nucleus-cluster


gcloud container clusters get-credentials nucleus-cluster

kubectl create deployment hello-server --image=gcr.io/google-samples/hello-app:2.0

kubectl expose deployment hello-server --type=LoadBalancer --port 8080

kubectl get service

---------------**CHECK YOUR SECOND PROGRESS NOW**------------------------------------------------------------------

gcloud container clusters delete nucleus-cluster

gcloud config set compute/zone us-central1-a

gcloud config set compute/region us-central1


***There is a big script in QWIKLABS manual, COPY and PASTE it.
After you do that. COPY AND PASTE below Commands
***

gcloud compute instance-templates create nginx-template \ --metadata-from-file startup-script=startup.sh


gcloud compute target-pools create nginx-pool

gcloud compute instance-groups managed create nginx-group --base-instance-name nginx --size 2 --template nginx-template --target-pool nginx-pool

gcloud compute instances list

gcloud compute firewall-rules create www-firewall --allow tcp:80

gcloud compute http-health-checks create http-basic-check


gcloud compute instance-groups managed \
       set-named-ports nginx-group \
       --named-ports http:80


gcloud compute backend-services create nginx-backend \
      --protocol HTTP --http-health-checks http-basic-check --global


gcloud compute backend-services add-backend nginx-backend \
    --instance-group nginx-group \
    --instance-group-zone us-central1-a \
    --global


gcloud compute url-maps create web-map \
    --default-service nginx-backend



gcloud compute target-http-proxies create http-lb-proxy \
    --url-map web-map


gcloud compute forwarding-rules create http-content-rule \
        --global \
        --target-http-proxy http-lb-proxy \
        --ports 80

gcloud compute forwarding-rules list



**copy http content rule IP address from output.
In new tab open the IP address
For Example:
http://34.120.223.29/
***

***IF THE WEBPAGE DISPLAYS THE INFORMATION CORRECTLY WITHOUT ANY ERROR THEN 
CHECK YOUR LAST PROGRESS***















