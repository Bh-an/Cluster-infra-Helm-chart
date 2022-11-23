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

- Kafka Explorarizatioin
```
kafkacat -b 192.168.58.2:30123 -t topic1 -L

echo "Am I receiving this message?" | kafkacat -P -b 192.168.58.2:30123 -t topic1
kafkacat -b 192.168.58.2:30123 -t topic1 -P test

kubectl exec -it infra-helm-kafka-0 -- bash

kafkacat -b 192.168.58.2:30123 -t topic1
kafkacat -b 192.168.58.2:30123 -t topic1 -C
kafkacat -b 192.168.58.2:30123 -L
```