# local-k8s-cluster

## Kubernetes Dashboard

### Intall

https://github.com/kubernetes/dashboard

```sh
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
```

### Create service accoount

https://github.com/kubernetes/dashboard/wiki/Creating-sample-user

### Login

```sh
# find token
$ kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | awk '{print $1}')
```

Login to the dashboard with found token.
