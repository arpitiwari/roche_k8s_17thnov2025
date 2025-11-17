# roche_k8s_17thnov2025

## Hypervisor vs Containers

![Containers Comparison](cont1.png)

## CRE Install Support

![CRE Installation](cre1.png)

## Checking Kernel Version

```bash
[ec2-user@ip-172-31-35-199 ~]$ uname -r
6.1.158-178.288.amzn2023.x86_64
```

## Checking Docker Version

```bash
[ec2-user@ip-172-31-35-199 ~]$ docker --version 
Docker version 25.0.13, build 0bab007

[ec2-user@ip-172-31-35-199 ~]$ docker version 
Client:
 Version:           25.0.13
 API version:       1.44
 Go version:        go1.24.9
 Git commit:        0bab007
 Built:             Mon Nov  3 00:00:00 2025
 OS/Arch:           linux/amd64
 Context:           default

Server:
 Engine:
    Version:          25.0.13
    API version:      1.44 (minimum version 1.24)
    Go version:       go1.24.9
    Git commit:       165516e
    Built:            Mon Nov  3 00:00:00 2025
```

## Docker Architecture

![Docker Architecture](d_arch.png)

## Docker Image Understanding

![Docker Image Concept](img1.png)

## Image Building Tool by Container Engines

![Image Building Tools](img2.png)

## Editing VSCode Config

```bash
nano ~/.config/code-server/config.yaml
```

## Pulling Docker Images

```bash
docker pull alpine 
docker images
docker pull quay.io/enxadahost/java
docker pull quay.io/redhattraining/hello-world-nginx
docker pull mcr.microsoft.com/ad-selection/azure/auction-service
docker pull mcr.microsoft.com/ad-selection/azure/auction-service:non-prod-4.3.0.0
```

## Creating Container with View

```bash
docker run --name ashuc1 -it -d alpine  
f92ec95d0d527342d4c4ab2e1652e51c32eba6ab2f109a0fd3dbbb2fa8f7a9ad

[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ docker ps
CONTAINER ID   IMAGE     COMMAND     CREATED              STATUS              PORTS     NAMES
74f8538ac396   alpine    "/bin/sh"   9 seconds ago        Up 9 seconds                  deb10
dec88d87c13e   alpine    "/bin/sh"   12 seconds ago       Up 11 seconds                 vinayak-alpine-first-run
9ec6ae801333   alpine    "/bin/sh"   12 seconds ago       Up 11 seconds                 harshc1
374873ddb556   alpine    "/bin/sh"   12 seconds ago       Up 12 seconds                 salilc1
64cf712ed4f4   alpine    "/bin/sh"   13 seconds ago       Up 12 seconds                 path51
311a20f32dde   alpine    "/bin/sh"   15 seconds ago       Up 14 seconds                 roshc1
```

## Building Docker Image

```bash
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ ls
java-app  python-app  website-apps

[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ docker build -t ashupython:v1 python-app/
[+] Building 11.5s (4/7)                                                                               docker:default
 => [internal] load build definition from Dockerfile                                                             0.0s
 => => transferring dockerfile: 410B                                                                             0.0s
 => [internal] load metadata for docker.io/library/python:latest                                                 2.1s
 => [internal] load .dockerignore                                                                                0.0s
 => => transferring context: 2B                                                                                  0.0s
 => [1/3] FROM docker.io/library/python:latest@sha256:e6b1f7011589cc717a5112e6fdb56217e9e734a57e4cb50216e912b06  9.3s
 => => resolve docker.io/library/python:latest@sha256:e6b1f7011
```

## Creating Container

```bash
[jivi@ip-172-31-35-199 jivi-common-apps]$ docker run -itd --name ashunc1 ashupython:v1  
4d81edcecd78983bbe7b94b16a06dd15ae0f7259a476050c818019dad0410b2a

[jivi@ip-172-31-35-199 jivi-common-apps]$ docker ps
CONTAINER ID   IMAGE                   COMMAND                  CREATED          STATUS          PORTS     NAMES
54eed0bda1e4   anjalipython:v1         "python /anjali-code…"   2 seconds ago    Up 1 second               anjalic2
0da5e805b036   pathpython:v1           "python /path-code/h…"   3 seconds ago    Up 1 second               nitinc2
4d81edcecd78   ashupython:v1           "python /ashu-code/h…"   4 seconds ago    Up 2 seconds              ashunc1
b77ad407065b   devpython:v1            "python /dev-code/he…"   31 seconds ago   Up 30 seconds             devc1
7310839f5768   ashishpython:v1         "python /ashish-code…"   39 seconds ago   Up 38 seconds             ashishnewc1
06f59f013f1b   sagar_python_image:v1   "python /sagar-code/…"   2 minutes ago    Up 2 minutes              sagar_py_image_container
```

## Some More Docker CLI Options

```bash
docker ps | grep ashu
docker logs ashunc1
docker logs -f ashunc1

[jivi@ip-172-31-35-199 jivi-common-apps]$ docker kill ashunc1
ashunc1

[jivi@ip-172-31-35-199 jivi-common-apps]$ docker start ashunc1
ashunc1

[jivi@ip-172-31-35-199 jivi-common-apps]$ docker ps
CONTAINER ID   IMAGE           COMMAND                  CREATED         STATUS                  PORTS     NAMES
9e10baf44b10   debpython:v1    "python /deb-code/he…"   4 minutes ago   Up Less than a second             deb10
4d81edcecd78   ashupython:v1   "python /ashu-code/h…"   5 minutes ago   Up 4 seconds                      ashunc1

[jivi@ip-172-31-35-199 jivi-common-apps]$ docker kill ashunc1
ashunc1

[jivi@ip-172-31-35-199 jivi-common-apps]$ docker rm ashunc1
ashunc1
```

## Pushing Image to Docker Registry

![Docker Push Process](push.png)

## Pushing Again

![Docker Push Success](push1.png)

## Pushing to Docker Hub

```bash
[ec2-user@ip-172-31-35-199 mypython-apps]$ docker tag ashupython:v1 docker.io/dockerashu/ashupython:v1

[ec2-user@ip-172-31-35-199 mypython-apps]$ docker login 
Log in with your Docker ID or email address to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com/ to create one.
You can log in with your password or a Personal Access Token (PAT). Using a limited-scope PAT grants better security and is required for organizations using SSO. Learn more at https://docs.docker.com/go/access-tokens/

Username: dockerashu
Password: 
WARNING! Your password will be stored unencrypted in /home/ec2-user/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded

[ec2-user@ip-172-31-35-199 mypython-apps]$ docker push docker.io/dockerashu/ashupython:v1
The push refers to repository [docker.io/dockerashu/ashupython]
e944a11d886d: Pushed 
6553e6a56eac: Pushed 
619f8a5f145e: Mounted from lilas2505/salilpython 
826bbffa4e22: Mounted from lilas2505/salilpython 
a44df98af09b: Mounted from lilas2505/salilpython 
9e2bd532623d: Mounted from lilas2505/salilpython
```

## using EKSctl to get k8s control plane access

```
[ec2-user@ip-172-31-35-199 ~]$  eksctl get clusters
NAME			REGION		EKSCTL CREATED
delvex-cluster-roche	ap-south-1	True
[ec2-user@ip-172-31-35-199 ~]$ kubectl   version 
Client Version: v1.34.2
Kustomize Version: v5.7.1
The connection to the server localhost:8080 was refused - did you specify the right host or port?
[ec2-user@ip-172-31-35-199 ~]$ eksctl utils write-kubeconfig --cluster=delvex-cluster-roche --kubeconfig=/home/ec2-user/.kube/config 
2025-11-17 10:13:37 [✔]  saved kubeconfig as "/home/ec2-user/.kube/config"
[ec2-user@ip-172-31-35-199 ~]$ 


```

## creating first pod 

```
kubectl  run  ashupod1  --image alpine --command ping 127.0.0.1 
pod/ashupod1 created
[ec2-user@ip-172-31-35-199 ashutoshh-common-apps]$ kubectl  get pods
NAME             READY   STATUS              RESTARTS      AGE
1-debasnan-pod   1/1     Running             0             5s
arpitpod1        0/1     Completed           3 (29s ago)   53s
ashishpod1       1/1     Running             0             11s
ashupod1         1/1     Running             0             11s
dasspod1         1/1     Running             0             6s
devpod1          1/1     Running             0             9s
gskpod1          1/1     Running             0             10s
jivipod1         1/1     Running             0             10s
mujpod1          1/1     Running             0             9s
nitinpod1        0/1     ContainerCreating   0             1s
salilpod1        1/1     Running             0             9s
vinayakpod1      1/1     Running             0             9s

```

### more kubectl commands 

```
 19  kubectl  get nodes
   20  kubectl  get pods
   21  kubectl  logs  ashupod1 
   22  history 
   23  kubectl  logs -f   ashupod1 

```
