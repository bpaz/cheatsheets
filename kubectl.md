---
title: Kubectl
layout: 2017/sheet
updated: 2017-11-27
category: kubernetes
prism_languages: [shell]
intro: > 
  [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) is the Kubernetes command line tool
---

{: .-no-hide}

## Installing

{: .-one-column}

```shell
sudo apt-get update && sudo apt-get install -y apt-transport-https
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubectl
```

## Cluster Management

### Get cluster information

```shell
kubectl cluster-info
```

### Configure the Context

```shell
kubectl config use-context my-cluster-name
```


## Deployments

### Display information of deployment

```shell
kubectl get deployments hello-world
```

### Expose a deployment

```shell
kubectl expose deployment hello-world --type=NodePort --name=example-service
```

## Creating objects

### From YAML file

```shell
kubectl create -f ./my-manifest.yaml
```

### From image

```shell
kubectl run nginx --image=nginx 
```

## Pods

### Show logs

```shell
kubectl logs -f my-pod  
```

### Execute command

```shell
kubectl exec my-pod -- ls /
```

### Port forward

```shell
kubectl port-forward my-pod 5000:6000  
```

### Get all pods with a specified label

```shell
kubectl get pods --selector=app=cassandra rc -o \
  jsonpath='{.items[*].metadata.labels.version}'
```

## Secrets

### Create secret from file

```shell
kubectl create secret generic db-user-pass --from-file=./username.txt --from-file=./password.txt
```

### Use secrets as environment variables

```yaml
 env:
    - name: SECRET_USERNAME
      valueFrom:
        secretKeyRef:
        name: mysecret
        key: username
```

References
----------

- <https://kubernetes.io/docs/tasks/tools/install-kubectl>
