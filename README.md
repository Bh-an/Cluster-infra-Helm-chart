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

- Expose Prometheus
```
kubectl expose service infra-helm-prometheus-server --type=NodePort --target-port=9090 --name=infra-helm-prometheus
minikube service infra-helm-prometheus
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