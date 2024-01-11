# README for Symmetric Database

kubectl create -f allover.yaml
kubectl config set-context $(kubectl config current-context) --namespace=allover

## Setup server1a database deployment

kubectl create -f server1a.yaml
### Delete server1a if any issues
kubectl delete deployment server1a
### Go back to the default namespace
kubectl config set-context $(kubectl config current-context) --namespace=default

