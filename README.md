# infra-helm

## Commands:

- Dependency Build
```
helm dependency build 
```

- Kafka
```
helm install kafka charts/kafka
helm uninstall kafka
```

- Elasticsearch
```
helm install ecs charts/elasticsearch
helm uninstall ecs
```

- Metrics-Server
```
helm install metrics charts/metrics-server
helm uninstall metrics
```

- Grafana
```
helm install grafana charts/grafana
helm uninstall grafana
```