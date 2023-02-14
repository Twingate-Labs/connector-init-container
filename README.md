# Twingate Connector Helm Chart

Command to Run:
```helm upgrade --install twingate-connector connector-init-container -n default --set twingate.apiKey="xxxx" --set twingate.account="xxxx.twingate.com" --set twingate.networkName="kube_test2"  --set connector.replicas=4 --values connector-init-container/values.yaml```