# Helm-chart for supporting cluster infrastructure

  This helm-chart contains some services and configurations useful for a kubernetes cluster. These include:
  - Kafka services - broker, cli support, zookeeper, zoonavigator ([reference](https://github.com/ricardo-aires/helm-charts/tree/main/charts/kafka "Kafka chart"))
  - Kibana server
  - Elasticsearch for logging with fluentd
  - Elasticsearch for stateless storage (dependency)
  - Prometheus stack with Grafana (dependency)
  - Metrics server (dependency)

## Usage:

Clone repo and move into working directory

- Dependency Build
```
helm dependency build 
```

- Helm Chart Install
```
helm install <release_name> -f Values.yaml <path_to_chart>
helm uninstall <release_name>
```

- Open Prometheus
```
kubectl port-forward prometheus-infra-helm-kube-prometheus-prometheus-0 9090
```

- Open Grafana Dashboard (go to 127.0.0.1)
```
kubectl port-forward <grafana-pod> 3000
kubectl get secret infra-helm-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```

- Use Kafka CLI

ssh into the pod:
```
kubectl exec -it kafka-cli -n kafka -- bash
```
example: creating a new topic
```
./bin/kafka-topics.sh --create --zookeeper zookeeper-svc:2181 --replication-factor 1 --partitions 2 --topic tasks
```

## Getting dashboard working

It would be much easier to see and understand and how the different components work with a dashboard, to set one up:

Apply the dashboard config:
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.6.1/aio/deploy/recommended.yaml
```
Forward port proxy:
```
kubectl proxy 
```
Get token for admin account (please understand what you're doing, this helmchart is only recommended for small non-commercial team projects in terms of security):
```
kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep kube-admin | awk '{print $1}')

```
Log into dashboard at:
```
http://localhost:8089/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

```
