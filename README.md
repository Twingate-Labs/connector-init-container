# Twingate Connector Helm Chart
**This is a prototype, not for production use. See [here](https://github.com/Twingate/helm-charts) for Twingate production Helm chart.**

## How to Use
Command to Run:
```helm upgrade --install twingate-connector connector-init-container -n default --set twingate.apiKey="xxxx" --set twingate.account="xxxx.twingate.com" --set twingate.networkName="kube_test2"  --set connector.replicas=4 --values connector-init-container/values.yaml```

Scaling:
``` 
kubectl scale statefulset twingate-connector --replicas=2
Or
helm upgrade --install twingate-connector connector-init-container -n default --set twingate.apiKey="xxxx" --set twingate.account="xxxx.twingate.com" --set twingate.networkName="kube_test2"  --set connector.replicas=10 --values connector-init-container/values.yaml
```

Summary:
1. Workflow:
    1. Init container provision connector
    2. Connector token stored in secret
    3. Connector application pod using the tokens stored in the secret
2. Stateful set
3. Antiaffinity set to preferredDuringSchedulingIgnoredDuringExecution
4. Service Account
5. Replicas can be defined
6. Pod die/kill auto recover

Potential Improvements:
1. Secret is overwritten for each new connector pod
   1. Can't access index info from helm easily
   2. Can be further improved if needed
2. Role is set as cluster admin, which is not ideal
   1. Cannot limit role access at the moment, as we are doing kubectl apply
   2. Can be improved if needed
3. Delete connector while pod die
   1. Require connector delete command
   2. Connector name - pod name map need to be stored somehow
   3. Could be complicated
   4. Can be further investigated if needed
4. Create init-container docker image

