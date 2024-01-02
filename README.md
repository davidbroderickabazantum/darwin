# README for Project Darwin

Darwin is an introduction to kubernetes control of docker images.

docker build -t node-image .
docker image tag node-image <dockerhubname>/node-image
docker push <dockerhubname>/node-image
kubectl apply -f manifest.yaml
kubectl get pods
