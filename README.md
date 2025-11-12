## K8-Project: MongoDB and Mongo Express Deployment

Hi everyone!
This project demonstrates how to deploy MongoDB and Mongo Express apps on a Kubernetes cluster using YAML manifests.
It covers how to manage multi-container applications with ConfigMaps, Secrets, and Services in Kubernetes.

Note: This project was built using Minikube in my local machine.

## 🧩 What’s Inside
- **MongoDB Deployment** → runs the MongoDB database  
- **Mongo Express Deployment** → web UI for MongoDB  
- **ConfigMap** → holds app-level configs (like DB host, DB name)  
- **Secret** → stores sensitive data (like DB username and password) in base64 format
- **Services** → expose both apps (internal and external access)

## 💡 Learning Takeaways
- **K8 Deployments:** How to create, deploy and manage multiple apps with Kubernetes Deployments
- **Service Configuration:** Configuration of ClusterIP and NodePort Services to allow IP and URL access
- **ConfigMap and Secrets:** How to manage ConfigMaps and Secrets and reference them in deployments
- **Minikube and Application Exposure:** Accessing web apps through Minikube

## 🧰 Tools Used
- Kubernetes (Minikube)
- Docker and Dockerhub
- MongoDB
- Mongo Express

## 🖥️ Demo Deployment Screenshots
## Terminal CLI after deployment
<img width="1214" height="815" alt="Mongo-Express-External-Service-CLI" src="https://github.com/user-attachments/assets/fb1510af-76f8-4653-bf04-e70cb6458259" />

## Mongo Express UI
<img width="1433" height="835" alt="Mongo-Express-UI" src="https://github.com/user-attachments/assets/9d605be2-9965-462c-830a-c16b3edaca16" />

## ⚙️ Deployment Steps:
## 1. Start MiniKube in your host machine
minikube start

## 1.1 Create Secrets in base64 format
echo -n "username" | base64

echo -n "password" | base64

## 2. Apply ConfigMap and Secret before executing the deployment files
kubectl apply -f mongo-configmap.yaml

kubectl apply -f mongo-secret.yaml

## 3. Deploy MongoDB and Mongo Express to create respective app pods
kubectl apply -f mongodb-deployment.yaml

kubectl apply -f mongo-express-deployment.yaml

## 4. Create Services
- **Internal Service for Mongo DB pod communication**

kubectl apply -f mongodb-service.yaml

- **External Service for Mongo Express UI access**

kubectl apply -f mongo-express-service.yaml

minikube service mongo-express service

URL: http://10.0.1.10:30000 => Sample

## Commands to verify Pod, Service, Secrets and Deployment configurations
kubectl get all

kubectl get pod

kubectl get service

kubectl get deployment

kubectl get secret

kubectl decribe service mongodb-service

## Commands: To view Extended Pod and Container details
kubectl describe pod

kubectl logs <POD_ID>

## Errors I faced and fixes provided after debugging:
- **Error:** CrashLoopBackOff error after deploying Mongo-Express
- **Cause:** MongoDB service name mismatch found in configmap and deployment file.
- **Fix:** Found MONGO_SERVER value in ConfigMap and Deployment: Changed the reference value of mongodb-configmap in mongo-express.yaml file.
