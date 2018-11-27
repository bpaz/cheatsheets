---
title: Minikube
layout: 2017/sheet
updated: 2017-11-27
category: kubernetes
prism_languages: [shell]
intro: > 
  [Minikube](https://github.com/kubernetes/minikube) is a tool that makes it easy to run Kubernetes locally. Minikube runs a single-node Kubernetes cluster inside a VM on your laptop for users looking to try out Kubernetes or develop with it day-to-day.
---

{: .-no-hide}

## Installing

{: .-one-column}

```shell
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

## Minikube commands

### Start

```shell
minikube start
```

### Start Minikube Service with 4 cpus and 8192 of memory

```shell
minikube start --cpus 4 --memory 8192 
```

### Show ip of the cluster

```shell
minikube ip
```

### Open dashboard

```shell
minikube dashboard
```

### Get the URL of service

```shell
minikube service --url SERVICE 
```

References
----------

- <https://github.com/kubernetes/minikube>
