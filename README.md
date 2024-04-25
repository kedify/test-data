# test-data


## Basic (1 SO, 1 SJ + TAs/CTAs)
```bash
kubectl apply -f https://raw.githubusercontent.com/zroubalik/test-data/main/resources/minutemetrics.yaml
kubectl apply -f https://raw.githubusercontent.com/zroubalik/test-data/main/resources/target.yaml
kubectl apply -f https://raw.githubusercontent.com/zroubalik/test-data/main/resources/so.yaml
kubectl apply -f https://raw.githubusercontent.com/zroubalik/test-data/main/resources/sj.yaml
kubectl apply -f https://raw.githubusercontent.com/zroubalik/test-data/main/resources/tas-ctas.yaml
```

### Bulk creation:
Following command creates 5 namespaces (named test-1 - test-5), in each namespace 25 SOs and 20 SJs
```bash
curl -s https://raw.githubusercontent.com/zroubalik/test-data/main/resources/create_resources.sh | \
bash -s -- 5 25 20 test
```
>Usage: ./create_resources.sh <num_namespaces> <scaled_objects_per_ns> <scaled_jobs_per_ns> [namespace_prefix]
