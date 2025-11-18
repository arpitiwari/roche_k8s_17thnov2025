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