# About

Files for "Learning Kubernetes: persistent storage with Minikube"

* [Learning Kubernetes: persistent storage with Minikube](https://martincarstenbach.wordpress.com/2019/06/07/learning-kubernetes-persistent-storage-with-minikube)


# Instructions

```shell
minikube start
```


# Create PV & PVC

```shell
kubectl apply -f k8/persistent-volumes.yml
```

```shell
kubectl get pc,pvc
```


# Build Docker Img

Use the minikube docker daemon, otherwise you will get: `ErrImagePull`

```shell
eval $(minikube -p minikube docker-env)
```

```shell
docker context show
```

```shell
docker build -t research:v2 docker/.
```

Verify:

```shell
minikube image ls
```

You should see: `docker.io/library/research:v2`


# Create Deployment

```shell
kubectl apply -f k8/research-deployment.yml
```

```shell
kubectl get deployments,pods
```

Files will be created at:


# SSH into minikube

List your files:

```shell
minikube ssh -- ls -ltr /data/research-vol/
```

# Cleanup

```shell
kubectl delete -f k8/research-deployment.yml
kubectl delete -f k8/persistent-volumes.yml
```
