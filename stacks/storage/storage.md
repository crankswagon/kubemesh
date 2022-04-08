# Storage
![storage](https://img.shields.io/badge/storage-minio-red)

We are using minio to provide a S3 API compliant backend for persistent storage.\
It's a way to abstract away the actual storage infrastucture. 

- In the example, we just have an SSD mounted directed to a k3s baremetal node, which is referenced as a [PV](https://kubernetes.io/docs/concepts/storage/persistent-volumes/).

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