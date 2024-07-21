# Machine-Learning-on-Kubernetes
##  **Step 1: Set up a Functional Kubernetes Cluster**
1. Open GKE terminal.
2. List all clusters:

    gcloud container clusters list

3. Create a Kubernetes cluster with three nodes using the following command:
   
   gcloud container clusters create kubia \
    --num-nodes=3 \
    --machine-type=n1-standard-1 \
    --region=us-west1-b
4. Check if nodes are correctly created:
   
   kubectl get nodes

   
