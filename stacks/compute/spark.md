# Compute
![compute](https://img.shields.io/badge/compute-spark-orange)

After `storage` and `registry` are set up on the cluster, we can start having a play with compute.\
First thing to try would be `apache spark` in clustered mode controlled by a driver pod running `jupyter notebook`. Hopefully this will feel somewhat similar to a `databricks notebook`.


- We should create a [PV](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) so that each time the driver pod is recreated, you don't lose your notebook data.

- In the example, this is targeting an `NFS`, but you can pick whatever storage backend you want.


## Usage

### *bring up the notebook stack*
```bash
kubectl apply -f ./stacks/compute/spark
```

### *verify statefulset successfully created*

```bash
kubectl get statefulset.apps/jupyter
```

### *test out the notebook* 

```bash
kubectl port-forward service/jupyter 8888:8888
```