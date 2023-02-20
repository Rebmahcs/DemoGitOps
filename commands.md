# Prepare cluster with argocd

## Create cluster
```kubectl create namespace argocd```  
```kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml```  
```kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'```

## Forward ports
```kubectl port-forward svc/argocd-server -n argocd 8080:443```  


# Get Password and login to argocd
```kubectl get -n argocd secrets argocd-initial-admin-secret -o yaml```  
```echo password | base64 --decode```

# Update Scaling and watch result
```kubectl patch deployment nginx-deployment -p '{"spec":{"replicas":3}}'```  
```kubectl describe deployment nginx-deployment -n demo-gitops```