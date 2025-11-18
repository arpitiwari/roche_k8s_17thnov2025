# roche_k8s_17thnov2025

### checking networking details of pods 

```
kubectl  apply -f k8s-yamls/deploy1.yaml 
deployment.apps/ashu-deploy configured
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ kubectl  get deploy 
NAME                 READY   UP-TO-DATE   AVAILABLE   AGE
arpit-deploy         1/1     1            1           39s
ashu-deploy          1/1     1            1           70s
dass-deploy          1/1     1            1           21s
debasnan-deploy      1/1     1            1           47s
dev-deploy           2/2     2            2           28s
harsh-deploy         1/1     1            1           50s
jivi-deploy          4/4     4            4           10s
nitin-deploy         2/2     2            2           29s

```
### creating service with expose command 

```
kubectl  expose  deployment ashu-deploy   --type LoadBalancer --name ashulb1  --port 80 --target-port 80  --dry-run=client -o yaml 
apiVersion: v1
kind: Service
metadata:
  labels:
    app: ashu-deploy
  name: ashulb1
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: ashu-deploy
  type: LoadBalancer
status:
  loadBalancer: {}
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ kubectl  expose  deployment ashu-deploy   --type LoadBalancer --name ashulb1  --port 80 --target-port 80  --dry-run=client -o yaml  >k8s-yamls/service1.yaml 
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ 

```

### creating service 

```
ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ kubectl create -f k8s-yamls/service1.yaml 
service/ashulb1 created
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ 
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ 
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ kubectl get service
NAME         TYPE           CLUSTER-IP       EXTERNAL-IP                                                                PORT(S)        AGE
arpitlb1     LoadBalancer   10.100.112.54    af58b580929c64cdb8094689467a4443-545020483.ap-south-1.elb.amazonaws.com    80:31690/TCP   54s
ashulb1      LoadBalancer   10.100.113.49    a483e77ee870b4d23a85ee9439a64dd5-202976125.ap-south-1.elb.amazonaws.com    80:31862/TCP   11s
devlb1       LoadBalancer   10.100.144.90    a2c79fbb7a5f34cab984690cbb15efaf-936540147.ap-south-1.elb.amazonaws.com    80:32305/TCP   11s
jivi         LoadBalancer   10.100.46.102    <pending>                                                                  80:32065/TCP   1s
kubernetes   ClusterIP      10.100.0.1       <none>                                                                     443/TCP        17h
rishlb1      LoadBalancer   10.100.222.36    ad668d4f211ee4a41bd96aea42d5d8aa-334147955.ap-south-1.elb.amazonaws.com    45:30328/TCP   3s
sagar-lb-1   LoadBalancer   10.100.156.120   ac8d25d8e806840de83599720e1ad2e5-1621246123.ap-south-1.elb.amazonaws.com   80:31353/TCP   23s
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ 

```
### deleting all resources 

```
kubectl  delete deploy,svc  --all

```

### creating a namespace 

```
[ec2-user@ip-172-31-35-199 ~]$ kubectl   get pods
No resources found in default namespace.
[ec2-user@ip-172-31-35-199 ~]$ 
[ec2-user@ip-172-31-35-199 ~]$ 
[ec2-user@ip-172-31-35-199 ~]$ kubectl  create  ns   ashu-project --dry-run=client -o yaml 
apiVersion: v1
kind: Namespace
metadata:
  name: ashu-project
spec: {}
status: {}
[ec2-user@ip-172-31-35-199 ~]$ kubectl  create  ns   ashu-project 
namespace/ashu-project created
[ec2-user@ip-172-31-35-199 ~]$ kubectl   get  ns
NAME              STATUS   AGE
ashu-project      Active   8s
default           Active   38h
dev-project       Active   2s
kube-node-lease   Active   38h
kube-public       Active   38h
kube-system       Active   38h
rish-project      Active   7s

```
### setting default ns 

```

[ec2-user@ip-172-31-35-199 ~]$ kubectl   config set-context --current --namespace ashu-project 
Context "boa-ashutoshh@delvex-cluster-roche.ap-south-1.eksctl.io" modified.
[ec2-user@ip-172-31-35-199 ~]$ 
[ec2-user@ip-172-31-35-199 ~]$ kubectl  get pods
No resources found in ashu-project namespace.
[ec2-user@ip-172-31-35-199 ~]$ 

```
## creating t2 webapp

### creating mysql db deployment file 

```
kubectl  create  deployment ashu-db  --image mysql --port 3306 --dry-run=client -o yaml  >ashu-t2webapp/db-deploy.yaml 

```
### deployed db 

```
 ls
ashu-t2webapp  java-app  k8s-yamls  python-app  website-apps
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ 
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ kubectl  apply -f  ashu-t2webapp/
deployment.apps/ashu-db created
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ kubectl   get  deploy 
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
ashu-db   1/1     1            1           45s
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ kubectl get pod
NAME                       READY   STATUS    RESTARTS   AGE
ashu-db-599d7cd98d-2zmjf   1/1     Running   0          82s
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ 

```
### debugging with db 

```
[ec2-user@ip-172-31-35-199 ~]$ kubectl  exec -it  ashu-db-599d7cd98d-2zmjf  -- /bin/bash 
bash-5.1# 
bash-5.1# 
bash-5.1# 
bash-5.1# mysql -u root -p 
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 9
Server version: 9.5.0 MySQL Community Server - GPL

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
mysql> 
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| ashu-db            |
| information_schema |


```
### creating db service to connect by apps 

```
kubectl   get deploy
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
ashu-db   1/1     1            1           10m
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ 
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ 
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ kubectl expose deploy  ashu-db  --type ClusterIP  --port 3306 --name ashudb-lb --dry-run=client  -o yaml  >ashu-t2webapp/db-svc.yaml 
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ 
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ kubectl apply -f ashu-t2webapp/
deployment.apps/ashu-db unchanged
service/ashudb-lb created
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ 

```
### creating webapp 

```
kubectl  create  deploy  ashu-webapp --image adminer --port 8080 --dry-run=client -o yaml >ashu-t2webapp/webapp-deploy.yaml 
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ 
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ kubectl  apply -f ashu-t2webapp/
deployment.apps/ashu-db unchanged
service/ashudb-lb unchanged
deployment.apps/ashu-webapp created
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ kubectl  get deploy
NAME          READY   UP-TO-DATE   AVAILABLE   AGE
ashu-db       1/1     1            1           27m
ashu-webapp   1/1     1            1           23s
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ kubectl  get svc
NAME        TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
ashudb-lb   ClusterIP   10.100.207.131   <none>        3306/TCP   15m

```

### creating svc 

```
kubectl  get deploy
NAME          READY   UP-TO-DATE   AVAILABLE   AGE
ashu-db       1/1     1            1           31m
ashu-webapp   1/1     1            1           3m52s
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ 
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ 
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ kubectl  expose deploy  ashu-webapp --type LoadBalancer --port 80 --target-port 8080 --name       ashu-web-lb  --dry-run=client -o yaml >ashu-t2webapp/web-svc.yaml 
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ 
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ 
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ 
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ kubectl apply -f ashu-t2webapp/
deployment.apps/ashu-db unchanged
service/ashudb-lb unchanged
service/ashu-web-lb created
deployment.apps/ashu-webapp unchanged
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ kubectl  get  svc
NAME          TYPE           CLUSTER-IP       EXTERNAL-IP                                                                PORT(S)        AGE
ashu-web-lb   LoadBalancer   10.100.64.19     a29574a6dd24542ab923616110c7aaef-1843863607.ap-south-1.elb.amazonaws.com   80:31869/TCP   51s
ashudb-lb     ClusterIP      10.100.207.131   <none>                                                                     3306/TCP       20m
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ 

```
### creating secret to store db password 

```
kubectl  create secret   generic  ashu-db-secret  --from-literal   myrootpass="Hello@12345" --dry-run=client    -o yaml 
apiVersion: v1
data:
  myrootpass: SGVsbG9AMTIzNDU=
kind: Secret
metadata:
  name: ashu-db-secret

```
### creating configMap 

```
kubectl create configmap ashu-db-config --from-literal  mydbname="ashu-db-new"  --dry-run=client -o yaml
apiVersion: v1
data:
  mydbname: ashu-db-new
kind: ConfigMap
metadata:
  name: ashu-db-config
[ec2-user@ip-172-31-35-199 ~]$ 


```
### doing all the deployment 

```
kubectl  apply -f ashu-t2webapp/
configmap/ashu-db-config created
deployment.apps/ashu-db created
secret/ashu-db-secret created
service/ashudb-lb created
service/ashu-web-lb created
deployment.apps/ashu-webapp created
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ 


=====>
kubectl    get  cm 
NAME               DATA   AGE
ashu-db-config     1      58s
kube-root-ca.crt   1      178m
[ec2-user@ip-172-31-35-199 ~]$ kubectl    get  secret
NAME             TYPE     DATA   AGE
ashu-db-secret   Opaque   1      71s
[ec2-user@ip-172-31-35-199 ~]$ kubectl    get  deploy
NAME          READY   UP-TO-DATE   AVAILABLE   AGE
ashu-db       1/1     1            1           79s
ashu-webapp   1/1     1            1           79s
[ec2-user@ip-172-31-35-199 ~]$ kubectl    get  po
NAME                           READY   STATUS    RESTARTS   AGE
ashu-db-6b9d979d6f-xjxft       1/1     Running   0          86s
ashu-webapp-6c445c87d4-9sk7l   1/1     Running   0          86s
[ec2-user@ip-172-31-35-199 ~]$ kubectl    get  svc
NAME          TYPE           CLUSTER-IP      EXTERNAL-IP                                                                PORT(S)        AGE
ashu-web-lb   LoadBalancer   10.100.94.189   a0d7afd753bee4c51af84aae5b745823-2068142561.ap-south-1.elb.amazonaws.com   80:31767/TCP   89s
ashudb-lb     ClusterIP      10.100.41.225   <none>                                                                     3306/TCP       89s
[ec2-user@ip-172-31-35-199 ~]$ kubectl    get  ep
Warning: v1 Endpoints is deprecated in v1.33+; use discovery.k8s.io/v1 EndpointSlice
NAME          ENDPOINTS             AGE
ashu-web-lb   192.168.23.185:8080   92s
ashudb-lb     192.168.43.186:3306   92s

```
