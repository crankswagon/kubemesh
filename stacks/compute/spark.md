# Compute
![compute](https://img.shields.io/badge/compute-spark-orange)

After `storage` and `registry` are set up on the cluster, we cna start having a play with compute.\
First thing to try would be `apache spark` in clustered mode controlled by a driver pod running `jupyter notebook`. Hopefully this will feel somewhat similar to a `databricks notebook`.


- First we should have some persistent storage [PV](https://kubernetes.io/docs/concepts/storage/persistent-volumes/).

- Alternatively, minio can be deployed using [minio operator](https://operator.min.io/) in clustered configuration accessing each node's disks using (directpv)[https://github.com/minio/directpv]. 

- Or.. you could just use actual **aws s3** :) 


## Usage

### *bring up the minio stack*
```bash
kubectl apply -f ./stacks/storage/minio
```

### *verify deployment and service*

```bash
kubectl get deployment minio-deployment
kubectl get svc minio-service
```

### *test out **aws cli s3** commands*
this assumes that you have a profile named `k3-s3` configured under `~/.aws/credentials`
the config are located within the [minio stack manifest](./minio/1_standalone_stack.yaml)

```bash
endpoint=$(kubectl get svc minio-service --output jsonpath='{.status.loadBalancer.ingress[0].ip}')
aws --profile k3-s3 --endpoint-url http://$endpoint:9000 s3 ls
aws --profile k3-s3 --endpoint-url http://$endpoint:9000 s3 mb s3://movies-data
aws --profile k3-s3 --endpoint-url http://$endpoint:9000 s3 ls s3://movies-data/delta/_delta_log/
```