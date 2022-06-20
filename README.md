# Kubernetes Deployment Tensorflow Flask Web Application
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
kubectl describe svc flask-app-service
```
**Getting Application Url**  <br>
```
minikube service flask-app-service --url
```
Kubernetes support two mthods to export services for external IP-addresses and internet: 1.NodePorts 2.Loadbalancers  <br>

**To expose application manually (without running svc yaml file) and run it from external IP address or internet, we acn expose our previous created deployment:**  <br>
```
kubectl expose deployment flask-app-deployment --type=NodePort --port=5000 
```
**Getting Url from manually set-up**  <br>
```
minikube service flask-app-deployment --url
```

**To monitor the execution of service: kubectl logs {pod name}**  <br>
```
kubectl logs deployment/flask-app-deployment
```
```
kubectl logs deployment/flask-app-deployment --follow --tail 1
```
```
kubectl describe pod/flask-app-deployment{-548d85c4bc-rtv67*** assigned label by Kubernetes}
```  
**To expose service with Loadbalancers to external IP-addresses:**  <br>
```
kubectl apply -f ./flask-app-lb.yaml
```
````
kubectl get svc flask-app-lb
```
```
curl http://$(minikube ip):{lb-Port e.g 31726}
```
## Set up Ingress on Minikube with the NGINX Ingress Controller <br>
```
minikube addons enable ingress 
```
```
kubectl get pods -n ingress-nginx 
```
```
kubectl create deployment web --image=masodatc/tensorflow-flask-web-application:01
```
```
kubectl expose deployment web --type=NodePort --port=8888 
```
```
kubectl get service web 
```
```
minikube service web 
```
**Create an Ingress:**  <br>
```
kubectl apply -f https://k8s.io/example-ingress.yaml 
```
```
kubectl get ingress
```

