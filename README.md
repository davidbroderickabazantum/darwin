# README for Project Darwin

Darwin is an introduction to kubernetes control of docker images.

docker build -t node-image .
docker image tag node-image <dockerhubname>/node-image
docker push <dockerhubname>/node-image
kubectl apply -f manifest.yaml
kubectl get pods

## Insecure Postgres

kubectl apply -f db-persistent-volume.yaml
kubectl apply -f db-volume-claim.yaml
kubectl apply -f db-configmap.yaml
kubectl apply -f db-deployment.yaml
kubectl apply -f db-service.yaml

