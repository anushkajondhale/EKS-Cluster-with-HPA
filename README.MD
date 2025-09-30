Here’s the code for your README:

# 🚀 AWS EKS: Horizontal Pod Autoscaler (HPA) with Load Testing

This project demonstrates how **Kubernetes’ Horizontal Pod Autoscaler (HPA)** automatically scales pods in **AWS EKS** based on real CPU load.

---

## 🎯 Project Goal
- Create an EKS Cluster  
- Deploy a sample web application  
- Expose via LoadBalancer  
- Install Metrics Server  
- Configure Horizontal Pod Autoscaler (HPA)  
- Generate CPU load  
- Observe autoscaling in action  

---

## 🛠️ Steps Overview

### 1️⃣ Create the EKS Cluster
```bash
eksctl create cluster --name my-cluster --region us-west-2

2️⃣ Deploy the Application
kubectl create deployment mywebd --image=vimal13/apache-webserver-php --dry-run=client -o yaml > deployment.yaml
kubectl apply -f deployment.yaml

3️⃣ Expose Deployment with LoadBalancer
kubectl expose deployment mywebd --type=LoadBalancer --name=mywebd-svc --port=80
kubectl get svc mywebd-svc


Check external access:

http://<EXTERNAL-IP>

4️⃣ Install Metrics Server
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
kubectl get pods -n kube-system
kubectl top pods

5️⃣ Configure Horizontal Pod Autoscaler
kubectl autoscale deployment mywebd --cpu-percent=50 --min=1 --max=10
kubectl get hpa
kubectl get hpa -w

6️⃣ Generate Load

Run a load generator pod:

kubectl run -i --tty load-generator --rm --image=busybox -- /bin/sh


Inside the pod, run:

while true; do wget -q -O- http://<EXTERNAL-IP>; done

7️⃣ Observe Autoscaling

Watch the HPA and pods in action:

kubectl get hpa -w
kubectl get pods
kubectl top pods

kubectl get hpa -w showing pod scaling

kubectl top pods with CPU utilization

Grafana/CloudWatch metrics (optional)

🔧 Tech Stack

AWS EKS (Elastic Kubernetes Service)

Kubernetes (HPA, Metrics Server)

Apache Web Server (PHP image)

Busybox (load generator)


📄 License

This project is licensed under the MIT License.


