# Course:   Google Cloud Platform Fundamentals - Core Infrastructure
## Module: Containers in the Cloud
## Lab: GCP Fundamentals: Getting Started with Kubernetes Engine

## Overview

In this lab, you create a Google Kubernetes Engine cluster containing several containers, each containing a web server. You place a load balancer in front of the cluster and view its contents.


## Objectives

In this lab, you learn how to perform the following tasks:

• Provision a Kubernetes cluster using Kubernetes Engine.

• Deploy and manage Docker containers using kubectl.


   ## Task 1: Confirm that needed APIs are enabled

1. Make a note of the name of your GCP project. This value is shown in the top bar of the Google Cloud Platform Console. It will be of the form qwiklabs-gcp- followed by hexadecimal numbers.

2. To confirm that both of these APIs are enabled use the gcloud command line:

    • Kubernetes Engine API

    • Container Registry API
    
 <div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">gcloud services list</div>
 
3. If the services are not avialable use the gcloud command line to run the following code.
 
 To enable service1, service2 and service3 on the current project run.
 
 <div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">gcloud services enable Kubernetes-Engine-API Container-Registry-API</div>
 
## Task 2: Start a Kubernetes Engine cluster
 
 1. For convenience, place the zone that Qwiklabs assigned you to into an environment variable called MY_ZONE. At the Cloud Shell prompt, type this partial command:
 
 <div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">export MY_ZONE=</div>
 
 followed by the zone that Qwiklabs assigned to you. Your complete command will look similar to this:
<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">export MY_ZONE=us-central1-a</div>

2. Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster **webfrontend** and configure it to run 2 nodes:
<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">gcloud container clusters create webfrontend --zone $MY_ZONE --numnodes 2</div>

    It takes several minutes to create a cluster as Kubernetes Engine provisions virtual machines for   you.
    
3. After the cluster is created, check your installed version of Kubernetes using the kubectl version command:
<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">kubectl version</div>

4. View your running nodes ,use gcloud command line and run the following code
<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;"> gcloud compute instances list</div>


    Your Kubernetes cluster is now ready for use.
    
 ## Task 3: Run and deploy a container
 
1. From your Cloud Shell prompt, launch a single instance of the nginx container. (Nginx is a popular web server.
<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">kubectl create deploy nginx --image=nginx:1.17.10</div>

    In Kubernetes, all containers run in pods. This use of the kubectl create command caused Kubernetes to create a deployment consisting of a single pod containing the nginx container. A Kubernetes deployment keeps a given number of pods up and running even in the event of failures among the nodes on which they run. In this command, you launched the default number of pods, which is 1.

    **Note**: If you see any deprecation warning about future version you can simply
ignore it for now and can proceed further.

2. View the pod running the nginx container:
<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">kubectl get pods</div>

3. Expose the nginx container to the Internet:
<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">kubectl expose deployment nginx --port 80 --type LoadBalancer</div>

    Kubernetes created a service and an external load balancer with a public IP address attached to it. The IP address remains the same for the life of the service. Any network traffic to that public IP address is routed to pods behind the service: in this case, the nginx pod.
    
    
4. View the new service:
<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">kubectl get services</div>
 
    You can use the displayed external IP address to test and contact the nginx container remotely.
    It may take a few seconds before the **External-IP** field is populated for your service. This is normal. Just run the kubectl get services command every few seconds until the field is populated.


5. Open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed.

6. Scale up the number of pods running on your service:
<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">kubectl scale deployment nginx --replicas 3</div>

    Scaling up a deployment is useful when you want to increase availableresources for an application that is becoming more popular.

7. Confirm that Kubernetes has updated the number of pods:
<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">kubectl get pods</div>

8. Confirm that your external IP address has not changed:
<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">kubectl get services</div>

9. Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding.