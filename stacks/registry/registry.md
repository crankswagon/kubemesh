# Registry
![registry](https://img.shields.io/badge/registry-docker-blue)

We are using docker registry to provide a self hosted local repo of docker images to launch pods with

- In the example, we are using an NFS share as the [PV](https://kubernetes.io/docs/concepts/storage/persistent-volumes/).


## Usage

### *update ./docker/0_storage.yaml with your configuration*

### *bring up the registry stack*
```bash
kubectl apply -f ./stacks/registry/docker
```

### *verify deployment and service*

```bash
kubectl get deployment docker-registry
kubectl get svc docker-registry-service
```

### *test out *docker registry* commands*

```bash
registry=$(kubectl get svc docker-registry-service --output jsonpath='{.status.loadBalancer.ingress[0].ip}')
curl http://$registry/v2/_catalog

# and if you have tls set up on an external load balancer
registry="registry.derp.work"
curl https://$registry/v2/_catalog
```
### try pushing something to your new registry
```bash
docker pull hello-world
docker tag hello-world $registry/hello-world:derp
docker push $registry/hello-world:derp

# you should now see that image in the repository 
curl https://$registry/v2/_catalog
```