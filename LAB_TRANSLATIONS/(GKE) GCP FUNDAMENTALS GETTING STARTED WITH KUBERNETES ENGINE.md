> # LAB: Google Cloud Fundamentals: Getting Started with GKE

## Task 1: Confirm that needed APIs are enabled

1. Make a note of the name of your GCP project. This value is shown in the top bar of the Google Cloud Platform Console.

    **COMMAND LINE:**

       gcloud projects list
      
2. In the GCP Console, on the Navigation menu (Navigation menu), click APIs & Services.

3. Scroll down in the list of enabled APIs, and confirm that both of these APIs are enabled:

    - Kubernetes Engine API
    - Container Registry API

    **COMMAND LINE:**

        gcloud services list

4. If either API is missing, click Enable APIs and Services at the top. Search for the above APIs by name and enable each for your current project

    **COMMAND LINE:**

        gcloud services enable container.googleapis.com

        gcloud services enable containerregistry.googleapis.com

        

## TASK 2: Start a Kubernetes Engine cluster
 1. For convenience, place the zone that Qwiklabs assigned you to into an environment variable called MY_ZONE.

       **COMMAND LINE:**

        export MY_ZONE=us-central1-a

2. Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes

   **COMMAND LINE:**

       gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2

3. After the cluster is created, check your installed version of Kubernetes

     **COMMAND LINE:**

        kubectl version

4. View your running nodes in the GCP Console. On the Navigation menu click Compute Engine > VM Instances.

      **COMMAND LINE:**

          gcloud compute instances list
 

## TASK 3: Run and deploy a container

1. Launch a single instance of the nginx container. (Nginx is a popular web server.)

    **COMMAND LINE:**

       kubectl create deploy nginx --image=nginx:1.17.10

2. View the pod running the nginx container

    **COMMAND LINE:**

        kubectl get pods
3. Expose the nginx container to the Internet

    **COMMAND LINE:**

       kubectl expose deployment nginx --port 80 --type LoadBalancer 
4. View the new service
5.  Open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed.
6. Scale up the number of pods running on your service

    **COMMAND LINE:**

       kubectl scale deployment nginx --replicas 3
7. Confirm that Kubernetes has updated the number of pods

    **COMMAND LINE:**

        kubectl get services
8. Confirm that your external IP address has not changed
9. Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding