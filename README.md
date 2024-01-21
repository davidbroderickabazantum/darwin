# README for Project Darwin

Darwin is an introduction to kubernetes control of docker images.

minikube start
minikube dashboard

docker build -t node-image .
docker image tag node-image <dockerhubname>/node-image
docker push <dockerhubname>/node-image
kubectl apply -f manifest.yaml
kubectl get pods

To scale up the deployment

kubectl scale deployment sample-node-app --replicas=5

To scale down the deployment to 1 

kubectl scale deployment sample-node-app --replicas=1

To rollout new containers - basic version for now

kubectl rollout restart deployment/sample-node-app

## Call the service to 'access' the sample-node-app

Node Service runs at port 80 on the cluster

minikube service node-service --url
Sample Response - http://127.0.0.1:61716



## Insecure Postgres

kubectl apply -f db-persistent-volume.yaml
kubectl apply -f db-volume-claim.yaml
kubectl apply -f db-configmap.yaml
kubectl apply -f db-deployment.yaml
kubectl apply -f db-service.yaml

## Secret Injection

kubectl create secret generic test-secret --from-literal='username=most-basic' --from-literal='password=ReallyC0mplexOne$'

## Stopping all deployments 
Key to remember, there is no concept of stop in Kubernetes

kubectl --namespace default scale deployment $(kubectl --namespace default get deployment | awk '{print $1}') --replicas 0


## Prod Credentials

kubectl create secret generic prod-db-secret --from-literal=username=production --from-literal=password=Secure1

kubectl apply -f manifest.yaml

Attach to the running pod and inspect

kubectl exec --stdin --tty sample-node-app-f4cf7f776-bspbq -- /bin/sh

-> Net outcome - secret injected and the pod can pick it up. It is not in the code for the pod and it is not known on the environment.


