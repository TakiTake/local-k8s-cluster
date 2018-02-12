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

## Jenkins

### Prepare mount point on host machine

Jenkins is statefull container so I need to use some persistent volume.
This time I chose ``hostPath`` because it's local test.

```sh
$ mkdir -p /Users/takeshitakizawa/data/jenkins
```

Sample code

```yaml
volumes:
- name: jenkins-home
  hostPath:
    path: /Users/takizawatakeshi/data/jenkins
```

### Access the Jenkins pod

I didn't know how to acces the pod with Kubernetes node IP and node port.
So I use ``kubectl port-forward`` to access to the pod direcly.

```sh
# Host:30000 -> Jenkins Pod's:8080
$ kubectl port-forward $(kubectl get pod | grep 'jenkins' | awk '{ print $1 }') 30000:8080
```

Now you can access Jenkins with http://localhost:30000/

### TODO

- Execute Job on the new Pod
- Execute gatling script on the new Pod
- Execute gatling script on the new Pod in parallel
- Generate gatling report from multiple simulation logs
