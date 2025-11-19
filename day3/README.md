# roche_k8s_17thnov2025

### clone sample webapp

```
git clone https://github.com/schoolofdevops/html-sample-app.git
```

### building docker image 

```
[ec2-user@ip-172-31-35-199 website-apps]$ ls
custom.dockerfile  html-sample-app  nginx.dockerfile

--->
docker build -t  rocheashutoshh.azurecr.io/ashuwebapp:v1  -f nginx.dockerfile .

 Building 0.3s (7/7) FINISHED                                                                              docker:default
 => [internal] load build definition from nginx.dockerfile                                                              0.0s
 => => transferring dockerfile: 233B                                                                                    0.0s
 => [internal] load metadata for docker.io/library/nginx:latest                                                         0.0s
 => [internal] load .dockerignore                                                                                       0.0s
 => => transferring context: 137B                                                                                       0.0s
 => [internal] load build context                                                                                       0.1s
 => => transferring context: 2.05MB                                                                                     0.0s
 => CACHED [1/2] FROM docker.io/library/nginx:l

 ```
 ### login to acr

 ```
 docker  login  rocheashutoshh.azurecr.io  -u  rocheashutoshh 
Password: 
WARNING! Your password will be stored unencrypted in /home/muj/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded

===>
 docker push  rocheashutoshh.azurecr.io/ashuwebapp:v1
```

### creating pod with private docker image 

```
kubectl  run ashupod1  --image  rocheashutoshh.azurecr.io/ashuwebapp:v1  --port 80 --dry-run=client   -o yaml 
apiVersion: v1
kind: Pod
metadata:

```

## image pull error options 

<img src="err.png">

### creating 

```
kubectl   create  secret   docker-registry  ashu-acr-creds --docker-username rocheashutoshh --docker-password "2+Aq"  --docker-server rocheashutoshh.azurecr.io  --dry-run=client   -o yaml

```

### creating 

```
kubectl apply -f acr-secret.yaml 
secret/ashu-acr-creds created
[ec2-user@ip-172-31-35-199 day3-deployments]$ kubectl  get secret
NAME             TYPE                             DATA   AGE
ashu-acr-creds   kubernetes.io/dockerconfigjson   1      7s
[ec2-user@ip-172-31-35-199 day3-deployments]$ 

```
###

```
kubectl replace -f demo-pod.yaml --force  ^C
[ec2-user@ip-172-31-35-199 day3-deployments]$ 
[ec2-user@ip-172-31-35-199 day3-deployments]$ 
[ec2-user@ip-172-31-35-199 day3-deployments]$ kubectl   get pods
NAME       READY   STATUS              RESTARTS   AGE
ashupod1   0/1     ContainerCreating   0          12s
[ec2-user@ip-172-31-35-199 day3-deployments]$ 

```

### creating deployment with secret 

```
kubectl  create  deployment ashu-dep1  --image rocheashutoshh.azurecr.io/ashuwebapp:v1 --port 80       --dry-run=client -o yaml 

```
