# roche_k8s_17thnov2025

### hypervisor vs contaienrs 

<img src="cont1.png">

### CRE install support 

<img src="cre1.png">

### checking kernel version 

```
[ec2-user@ip-172-31-35-199 ~]$ uname -r
6.1.158-178.288.amzn2023.x86_64

```
### checking docker version 

```
[ec2-user@ip-172-31-35-199 ~]$ docker --version 
Docker version 25.0.13, build 0bab007
[ec2-user@ip-172-31-35-199 ~]$ 
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
### docker architecture 

<img src="d_arch.png">

