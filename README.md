# Plan of training 

<img src="plan.png">

## checking k8s clsuter connection 

```
===
kubectl  get  nodes
NAME         STATUS   ROLES                  AGE   VERSION
masternode   Ready    control-plane,master   25h   v1.22.2
node1        Ready    <none>                 25h   v1.22.2
node2        Ready    <none>                 25h   v1.22.2

===
kubectl  config get-contexts    
CURRENT   NAME                          CLUSTER      AUTHINFO           NAMESPACE
*         kubernetes-admin@kubernetes   kubernetes   kubernetes-admin   ashu-space

===

kubectl delete pods --all
pod "ashupod1" deleted
pod "webpod1" deleted
 fire@ashutoshhs-MacBook-Air  ~  

```

