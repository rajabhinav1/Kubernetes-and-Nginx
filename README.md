
You need to have docker and Kubernetes in your system then you can proceed with configuring to deploy a single node of clusters.


![image](https://github.com/rajabhinav1/Kubernetes-and-Nginx/assets/27865950/be003aea-a11c-46e4-84e8-c784f3ea2cbb)

#For the program 1

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

#For the program 2

Configure using gibash

# for ARM systems, set ARCH to: `arm64`, `armv6` or `armv7`
ARCH=amd64
PLATFORM=windows_$ARCH

curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.zip"

# (Optional) Verify checksum
curl -sL "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_checksums.txt" | grep $PLATFORM | sha256sum --check

unzip eksctl_$PLATFORM.zip -d $HOME/bin

rm eksctl_$PLATFORM.zip

eksctl create cluster --name my-cluster --version 1.18 --region us-west-2 --nodegroup-name my-nodes --node-type t3.medium --nodes 3 --nodes-min 1 --nodes-max 4 --managed

docker build -t my-app:v1 .
aws ecr create-repository --repository-name my-app
$(aws ecr get-login --no-include-email --region us-west-2)
docker tag my-app:v1 <account-id>.dkr.ecr.us-west-2.amazonaws.com/my-app:v1
docker push <account-id>.dkr.ecr.us-west-2.amazonaws.com/my-app:v1


kubectl apply -f deployment.yaml
kubectl apply -f deployment2.yaml
kubectl get svc
kubectl scale deployment my-app --replicas=3
kubectl delete -f deployment.yaml
kubectl delete -f deployment2.yaml
eksctl delete cluster --name my-cluster












