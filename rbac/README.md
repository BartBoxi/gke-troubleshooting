# LAB

## Test 1

#This lab is forked from another github user - https://github.com/pradeepnss/gke-troubleshooting/tree/master/rbac. 
#This lab was forked and updated to make sure that manual for that is valid in 2024. 

### Create service account and pod using that service account

```sh
kubectl create serviceaccount test --namespace=default
kubectl run nginx-1 \
    --image=nginx:latest \
    --namespace=default \
    --overrides='{
        "spec": {
            "template": {
                "spec": {
                    "serviceAccountName": "test"
                }
            }
        }
    }'
```

### Exec into the pod

```sh
kubectl get pod
kubectl exec -it PODNAME bash
```

### Target API server
```sh
apt-get update && apt-get install -y curl
curl -ik https://kubernetes.default.svc.cluster.local/version
```

### Get list of pods in default namespace
```sh
curl -ik \
     -H "Authorization: Bearer $(cat /var/run/secrets/kubernetes.io/serviceaccount/token)" \
     https://kubernetes.default.svc.cluster.local/api/v1/namespaces/default/pods
```

Now how do you fix this so that from this pod we can perform list of pods in default namespace ?

Solution will be provided as a separate file for that LAB. 

Thanks 
Bart

