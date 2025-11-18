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
