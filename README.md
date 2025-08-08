# Machine-Learning-on-Kubernetes
##  **Step 1: Set up a Functional Kubernetes Cluster**
1. Open GKE terminal.
2. Start minikube in Google Cloud Platform
   
         minikube start
   
3. Create requirements.txt file using the following command:

        nano requirements.txt
   
Enter the following contents in requirements.txt:

        Flask==1.1.1
        gunicorn==19.9.0
        itsdangerous==1.1.0
        Jinja2==2.10.1
        MarkupSafe==1.1.1
        Werkzeug==0.15.5
        numpy==1.19.5
        scipy>=0.15.1
        scikit-learn==0.24.2
        matplotlib>=1.4.3
        pandas>=0.19
        flasgger==0.9.4
        
Upload logreg.pkl file which we got from ML.ipynb and using data set

- Click the three dots in the top-right part of the Cloud Shell Terminal
  
- Choose upload and upload the logreg.pkl file

4. Create flask_api.py file using the command:

           nano flask_api.py
   
or, you can also uplaod it from flask_api.py file  
                  
5. Create Dockerfile using the command:
   
           nano Dockerfile

Enter the following contents in Dockerfile:

        FROM python:3.8-slim
        WORKDIR /app
        COPY . /app
        EXPOSE 5000
        RUN pip install -r requirements.txt
        CMD ["python", "flask_api.py"]

6. Build the Docker image using the command:

           sudo docker build -t ml_app_docker .

7. Run the Docker container using the command:

           docker container run -p 5000:5000 ml_app_docker

9. Preview the application:

- In the upper-right side of the terminal, click the eye-shaped button and then click "Preview on port 5000".


  ![Screenshot 2024-07-21 200204](https://github.com/user-attachments/assets/0bb0bba2-73f8-45e5-a2dd-09debc4eb17d)

- Add **/apidocs/** at the end of the link to access the running ml-app.

![Screenshot 2024-07-21 203724](https://github.com/user-attachments/assets/69aa8f2f-4b7d-451b-a746-6e859e4c9dbb)


10. Make predictions for a group of customers (test data) via a POST request:

- Upload the test data file containing the same parameters in a similar order.
- Execute to display the results.

   ### **Step 1.1. Stop/kill the running container:**

- List running Docker containers using the command:

         docker ps

- Use the command to kill the running container

        docker kill <CONTAINER ID>


   ## Step 2: Push the image to your docker hub

1. Log in to Docker Hub:

          docker login
   
3. Tag the Image:

         docker tag ml_app_docker nazninnahar054/ml_docker:latest

4. Push the Image:

         docker push nazninnahar054/ml_docker:latest

5. Verify the image exists locally by listing your Docker images:

         docker images

![Screenshot 2024-07-21 202328](https://github.com/user-attachments/assets/06783a5c-6f45-4d24-994e-4884b0c5a5f8)

**P.S. Before login to docker build the image if pushing isn't working**

   ## Step 3: Deploy your ML app to GKE

Use the GKE we have created in Step 1

1. Create a deployment.yaml with the following contents.

         nano deployment.yaml
   
   then write [this](deployment.yaml) content 
   
3. Create deployment with the above file.

         kubectl apply -f ml-app-deployment.yaml

4. Wait for couple minutes and list all the pods created

         kubectl get deployments
         kubectl get pods

5. Create a service.yaml

         nano service.yaml
   
then write [this ](https://github.com/NazninNaharSr/Machine-Learning-on-Kubernetes/blob/main/service.yaml)content 
   
6. Create service with the above file

         kubectl apply -f ml-app-service.yaml

7. Get service external ip

         kubectl get services

8. Access using browser:
   
         external-ip/apidocs


















   
