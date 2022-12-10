# infra-helm

## Commands:

- Dependency Build
```
helm dependency build 
```

- Helm Chart Install
```
helm install infra-helm -f Values.yaml .
helm uninstall infra-helm
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

- Kafka Configuration

# ssh into the pod:
kubectl exec -it kafka-cli -n kafka -- bash
```
```bash
# create a new topic
./bin/kafka-topics.sh --create --zookeeper zookeeper-svc:2181 --replication-factor 1 --partitions 2 --topic tasks


```