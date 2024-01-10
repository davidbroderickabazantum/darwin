# Limit Access to Pods

When pods start up they get access to secrets that enable them perform their work. 
In the case of wooramel, it will get access to a database that has PCI rich data, so a solution is needed.

## Pod Security Admission

kubectl label --overwrite ns --all \
    pod-security.kubernetes.io/enforce=baseline \
    pod-security.kubernetes.io/enforce=baseline

## Use RBAC Authorization
To be setup in next tutorial
