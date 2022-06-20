# Kubenetes Deployment Tensorflow Flask Web Application
**Steps:** <br>
-RUN following command to create deployment and Service in Kubernetes Kluster <br>
$ kubectl apply -f ./run-my-flask-app.yaml <br>
$ kubectl apply -f ./flask-app-svc.yaml <br>
<br>
Once our application service created to check the resources run:<br>
- $ kubectl get pod -w <br>
- $ kubectl get all <br>
- $ kubectl describe svc flask-app-deployment <br>
To expose application from external IP address and internet run:<br>
- $ kubectl expose deployment flask-app-deployment --type=NodePort --port=5000<br>
- $ minikube service flask-app-deployment --url<br>
- <br>
To monitor the execution of service:<br>
- $ kubectl logs deployment/flask-app-deployment<br>
- $ kubectl logs deployment/flask-app-deployment --follow --tail 1<br>
- $ kubectl describe pod/flask-app-deployment{-548d85c4bc-rtv67*** assigned label by Kubernetes}<br>

