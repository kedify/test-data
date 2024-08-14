# test-data


## Basic: Sample SO and SJ
```bash
kubectl apply -f https://raw.githubusercontent.com/zroubalik/test-data/main/resources/minutemetrics.yaml
kubectl apply -f https://raw.githubusercontent.com/zroubalik/test-data/main/resources/target.yaml
kubectl apply -f https://raw.githubusercontent.com/zroubalik/test-data/main/resources/so.yaml
kubectl apply -f https://raw.githubusercontent.com/zroubalik/test-data/main/resources/sj.yaml
```

## Cluster/TriggerAuthentications
Creates 8 TAs and 8 CTAs
```bash
kubectl apply -f https://raw.githubusercontent.com/zroubalik/test-data/main/resources/tas-ctas.yaml
```

## Bulk creation:
Following command creates 5 namespaces (named test-1 - test-5), in each namespace 25 SOs and 20 SJs
```bash
curl -s https://raw.githubusercontent.com/zroubalik/test-data/main/resources/create_resources.sh | \
bash -s -- 5 25 20 test
```
>Usage: ./create_resources.sh <num_namespaces> <scaled_objects_per_ns> <scaled_jobs_per_ns> [namespace_prefix]


## Simulating a k8s cluster that has also some other workloads:
```
# create a cluster w/ 5 worker nodes
k3d cluster delete ; k3d cluster create --servers 7 --no-lb --k3s-arg "--disable=traefik,servicelb,local-storage@server:*"
kubectl wait --for=condition=Ready nodes --all --timeout=600s

# install kedify
kubectl kedify i --email foo@bar -y

curl -s https://raw.githubusercontent.com/zroubalik/test-data/main/resources/create_resources.sh | \
OTHER_DEPLOYMENTS=1 \
bash -s -- 5 15 20 scale

# create 8 namespaces (t-1 - t-8) and in each 7 deployments and 1 stateful set (with pause container)
curl -s https://raw.githubusercontent.com/zroubalik/test-data/main/resources/create_resources.sh | \
OTHER_DEPLOYMENTS=7 \
OTHER_STATEFUL_SETS=1 \
bash -s -- 8 0 0 t
```
