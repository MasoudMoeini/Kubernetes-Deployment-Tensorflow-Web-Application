# Kubernetes Deployment Tensorflow Flask Web Application using Minikube
**Steps:**  <br>
Clone Repo and **RUN** following command to create deployment and Service in Kubernetes cluster: <br>
```
kubectl apply -f ./flask-app-deployment.yaml 
```
```
kubectl get pods
```
```
kubectl apply -f ./flask-app-svc.yaml 
```
**Once application service created, to check the resources run:**  <br>
```
kubectl get pods -w 
```
```
kubectl get all 
```
```
kubectl get service flask-app-deployment
```
```
kubectl describe svc flask-app-deployment
```
**Getting Application Url**  <br>
```
minikube service flask-app-deployment --url
```
Kubernetes support two mthods to export services for external IP-addresses and internet: 1.NodePorts 2.Loadbalancers  <br>

To deploy and expose application manually (without running svc yaml file) and run it from external IP address or internet:  <br>
```
kubectl create deployment flask-web-app --image=masodatc/tensorflow-flask-web-application:01
kubectl expose deployment flask-web-app --type=NodePort --port=5000 
kubectl scale deployment flask-web-app --replicas 3
```
Scaling a Deployment:
```
kubectl scale deployment/flask-web-app --replicas=10
kubectl autoscale deployment/flask-web-app --min=10 --max=15 --cpu-percent=80
```
```
kubectl get service flask-web-app 
minikube service flask-web-app --url
```
**Getting Url from manually set-up**  <br>
```
minikube service flask-web-app --url
```
**To monitor the execution of service: kubectl logs {pod name}**  <br>
```
kubectl logs pod/flask-app-deployment
```
```
kubectl logs pod/flask-app-deployment --follow --tail 1
```
```
kubectl describe pod/flask-app-deployment{-548d85c4bc-rtv67*** assigned label by Kubernetes}
```  
**To expose service with Loadbalancers to external IP-addresses:**  <br>
```
kubectl apply -f ./flask-app-lb.yaml
```
```
kubectl get svc flask-app-deployment
```
```
curl http://$(minikube ip):{lb-Port e.g 31726}
```
Delete resources <br>
```
kubectl delete all --all --all-namespaces
```
```
minikube delete && minikube start --driver=hyperkit
```
## Set up Ingress on Minikube with the NGINX Ingress Controller <br>
```
minikube addons enable ingress 
```
```
kubectl get pods -n ingress-nginx 
```
```
kubectl apply -f ./flask-app-deployment.yaml 
```
```
kubectl apply -f ./flask-app-svc.yaml 
```
```
kubectl get service flask-app-deployment
```
```
minikube service flask-app-deployment --url
```
**Create an Ingress:**  <br>
```
kubectl apply -f example-ingress.yaml
```
```
kubectl get ingress
```
Updating /etc/hosts file with "192.168.64.4 hello-world.info" <br>
- On macOs ->[Introduction](https://help.nexcess.net/en_US/miscellaneous/how-to-find-the-hosts-file-on-my-mac)
```
curl hello-world.info
```
```
kubectl describe ingress example-ingress
```
