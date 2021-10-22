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

### checking labels from command line 

```
kubectl  get  po --show-labels
NAME      READY   STATUS    RESTARTS   AGE     LABELS
webpod1   1/1     Running   0          4m38s   x1=ashuapp1

```

## Service NodePort 

<img src="np.png">

## creating nodeport service 

```
kubectl  create  service 
Create a service using specified subcommand.

Aliases:
service, svc

Available Commands:
  clusterip    Create a ClusterIP service.
  externalname Create an ExternalName service.
  loadbalancer Create a LoadBalancer service.
  nodeport     Create a NodePort service.
  
```

### creating 

```
 kubectl  create  service  nodeport  ashus1  --tcp  1234:80  --dry-run=client -o yaml 
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    app: ashus1
  name: ashus1
spec:
  ports:
  - name: 1234-80
    port: 1234
    protocol: TCP
    targetPort: 80
  selector:
    app: ashus1
  type: NodePort
status:
  loadBalancer: {}
 fire@ashutoshhs-MacBook-Air  ~/Desktop/k8s_app_deploy  kubectl  create  service  nodeport  ashus1  --tcp  1234:80  --dry-run=client -o yaml   >ashusvc1.yaml
 
 ```
 
 ### matching service selector to label of POD 
 
 <img src="label.png">
 
 ### Deployed service yaml 
 
 <img src="svcdep.png">
 
 ```
 kubectl apply -f  ashusvc1.yaml 
service/ashus1 created
 fire@ashutoshhs-MacBook-Air  ~/Desktop/k8s_app_deploy  kubectl  get service 
NAME     TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
ashus1   NodePort   10.105.229.142   <none>        1234:32328/TCP   8s

```

