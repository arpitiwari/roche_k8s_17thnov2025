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