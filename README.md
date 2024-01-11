![image](https://github.com/rajabhinav1/Kubernetes-and-Nginx/assets/27865950/272db89b-7d99-455d-a959-2283c4826c98)

You need to have docker and kubernetes in your system then you can proceed with configuring to deploy a single node of clusters on your kubernetes instance.


![image](https://github.com/rajabhinav1/Kubernetes-and-Nginx/assets/27865950/be003aea-a11c-46e4-84e8-c784f3ea2cbb)

For the program 1

Create a file named Dockerfile with the following content:
FROM nginx:latest
COPY . /usr/share/nginx/html
Build the Docker image:
docker build -t my-nginx-image:v1 .
minikube docker-env
eval $(minikube -p minikube docker-env)
docker build -t my-nginx-image:v1 .
kubectl apply -f nginx-deployment.yaml
kubectl get pods
kubectl autoscale deployment nginx-deployment --cpu-percent=50 --min=2 --max=5
kubectl get hpa
kubectl delete deployment nginx-deploymentDelete the HPA:
kubectl delete hpa nginx-deployment

For the program 2
