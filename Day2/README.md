# RedHat OpenShift Container Platform (OCP)
For training/consulting/coaching, you may reach me

<pre>
    jegan@tektutor.org
    +91 822-000-5626 (WhatsApp)
</pre>

## ⛹️‍♂️ Lab - Creating a NodePort external service for nginx deployment

```
oc delete project jegan
oc new-project jegan
oc new-app twalter/openshift-nginx:stable --name nginx
oc expose deploy/nginx --type=NodePort --port=80
```

The expected output is

<pre>
jegan@tektutor:~$ <b>oc expose deploy/nginx --type=NodePort --port=80</b>
service/nginx exposed
jegan@tektutor:~$ <b>oc get svc</b>
<b>NAME    TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE</b>
nginx   NodePort   172.30.216.75   <none>        80:30327/TCP   4s
jegan@tektutor:~$ <b>oc describe svc/nginx</b>
Name:                     nginx
Namespace:                jegan
Labels:                   app=nginx
                          app.kubernetes.io/component=nginx
                          app.kubernetes.io/instance=nginx
Annotations:              <none>
Selector:                 deployment=nginx
Type:                     NodePort
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       172.30.216.75
IPs:                      172.30.216.75
Port:                     <unset>  80/TCP
TargetPort:               80/TCP
NodePort:                 <unset>  30327/TCP
Endpoints:                <b>10.128.2.23:80,10.128.2.26:80,10.128.2.27:80 + 2 more...</b>
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
</pre>

## ⛹️‍♀️ Lab - Accessing the nginx NodePort service

Nginx NodePort service can be accessed using one the below commands

```
curl http://master-1.tektutor.tektutor.org:30327
curl http://master-2.tektutor.tektutor.org:30327
curl http://master-3.tektutor.tektutor.org:30327
curl http://worker-1.tektutor.tektutor.org:30327
curl http://worker-2.tektutor.tektutor.org:30327
curl http://192.168.122.13:30327
curl http://192.168.122.228:30327
curl http://192.168.122.89:30327
curl http://192.168.122.36:30327
curl http://192.168.122.222:30327
```

The expected output is

<pre>
jegan@tektutor:~$ <b>oc get nodes -o wide</b>
<b>NAME                             STATUS   ROLES           AGE    VERSION           INTERNAL-IP       EXTERNAL-IP   OS-IMAGE                                                       KERNEL-VERSION                 CONTAINER-RUNTIME</b>
master-1.tektutor.tektutor.org   Ready    master,worker   117m   v1.22.3+fdba464   192.168.122.13    <none>        Red Hat Enterprise Linux CoreOS 49.84.202202081504-0 (Ootpa)   4.18.0-305.34.2.el8_4.x86_64   cri-o://1.22.1-14.rhaos4.9.git7486bc8.el8
master-2.tektutor.tektutor.org   Ready    master,worker   118m   v1.22.3+fdba464   192.168.122.228   <none>        Red Hat Enterprise Linux CoreOS 49.84.202202081504-0 (Ootpa)   4.18.0-305.34.2.el8_4.x86_64   cri-o://1.22.1-14.rhaos4.9.git7486bc8.el8
master-3.tektutor.tektutor.org   Ready    master,worker   118m   v1.22.3+fdba464   192.168.122.89    <none>        Red Hat Enterprise Linux CoreOS 49.84.202202081504-0 (Ootpa)   4.18.0-305.34.2.el8_4.x86_64   cri-o://1.22.1-14.rhaos4.9.git7486bc8.el8
worker-1.tektutor.tektutor.org   Ready    worker          99m    v1.22.3+fdba464   192.168.122.36    <none>        Red Hat Enterprise Linux CoreOS 49.84.202202081504-0 (Ootpa)   4.18.0-305.34.2.el8_4.x86_64   cri-o://1.22.1-14.rhaos4.9.git7486bc8.el8
worker-2.tektutor.tektutor.org   Ready    worker          100m   v1.22.3+fdba464   192.168.122.222   <none>        Red Hat Enterprise Linux CoreOS 49.84.202202081504-0 (Ootpa)   4.18.0-305.34.2.el8_4.x86_64   cri-o://1.22.1-14.rhaos4.9.git7486bc8.el8

jegan@tektutor:~$ <b>oc describe svc/nginx</b>
Name:                     nginx
Namespace:                jegan
Labels:                   app=nginx
                          app.kubernetes.io/component=nginx
                          app.kubernetes.io/instance=nginx
Annotations:              <none>
Selector:                 deployment=nginx
Type:                     NodePort
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       172.30.216.75
IPs:                      172.30.216.75
Port:                     <unset>  80/TCP
TargetPort:               80/TCP
NodePort:                 <unset>  30327/TCP
Endpoints:                10.128.2.23:80,10.128.2.26:80,10.128.2.27:80 + 2 more...
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>

jegan@tektutor:~$ <b>curl 192.168.122.13:31030</b>
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
Welcome to nginx!
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
</pre>

## ⛹️‍♂️ Lab - Creating a LoadBalancer external service

As we can't create more than one service type per deployment, we need to delete the existing NodePort service for the nginx deployment before we can create LoadBalancer service.

```
oc get svc
oc delete svc nginx
```

The expected output is

<pre>
jegan@tektutor:~$ <b>oc get svc</b>
<b>NAME    TYPE       CLUSTER-IP    EXTERNAL-IP   PORT(S)          AGE</b>
nginx   NodePort   172.30.8.94   <none>        8081:31030/TCP   14h
jegan@tektutor:~$ oc delete svc nginx
service "nginx" deleted
</pre>

Now let's create the LoadBalancer external service for nginx deployment

```
oc expose deploy nginx --type=LoadBalancer --port=8081
```

The expected output is
<pre>
jegan@tektutor:~$ <b>oc get deploy</b>
<b>NAME    READY   UP-TO-DATE   AVAILABLE   AGE</b>
nginx   5/5     5            5           14h
jegan@tektutor:~$ <b>oc expose deploy nginx --type=LoadBalancer --port=8081</b>
service/nginx exposed
jegan@tektutor:~$ <b>oc get svc</b>
<b>NAME    TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE</b>
nginx   LoadBalancer   172.30.94.17   <pending>     8081:31918/TCP   4s
jegan@tektutor:~$ <b>oc describe svc nginx</b>
Name:                     nginx
Namespace:                jegan
Labels:                   app=nginx
                          app.kubernetes.io/component=nginx
                          app.kubernetes.io/instance=nginx
Annotations:              <none>
Selector:                 deployment=nginx
Type:                     LoadBalancer
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       172.30.94.17
IPs:                      172.30.94.17
Port:                     <unset>  8081/TCP
TargetPort:               8081/TCP
NodePort:                 <unset>  31918/TCP
Endpoints:                10.128.2.23:8081,10.128.2.26:8081,10.128.2.27:8081 + 2 more...
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
</pre>4. 

## ⛹️‍ Lab - Accessing the LoadBalancer external service

LoadBalancer type of Service is useful in creating in provisioning a LoadBalancer in AWS/Azure/GCP, etc

But when we create a LoadBalancer service in local openshift cluster, it works like a NodePort service. 

```
curl master-1.tektutor.tektutor.org:31918
curl master-2.tektutor.tektutor.org:31918
curl master-3.tektutor.tektutor.org:31918
curl worker-1.tektutor.tektutor.org:31918
curl worker-2.tektutor.tektutor.org:31918
```

The expected output is

<pre>
jegan@tektutor:~$ <b>curl master-1.tektutor.tektutor.org:31918</b>
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
Welcome to nginx!
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
</pre>

## ⛹️‍♀️ Lab - Creating a ClusterIP Service for nginx deployment

We need to delete any existing service for nginx deployment before we can create the ClusterIP service for nginx deployment.

```
oc delete svc/nginx
```

Now let's create the ClusterIP internal service for nginx deployment

```
oc expose deploy/nginx --type=ClusterIP --port=8081
oc get svc
oc describe svc/nginx 
```

As ClusterIP service is an internal service, it is accessible only within the OpenShift cluster as opposed to NodePort or LoadBalancer services.  Hence we need to attempt to access the ClusterIP from a Pod shell as the Pod is running within the Cluster, service discovery works as expected.

Let's create a dnstest pod to access the nginx clusterip service from its shell

```
oc run dnstest -it --restart Never --rm --image tutum/dnsutils bash
```
The expected output is

<pre>
jegan@tektutor:~$ <b>oc delete svc nginx</b>
service "nginx" deleted
jegan@tektutor:~$ <b>oc expose deploy/nginx --type=ClusterIP --port=8081</b>
service/nginx exposed
jegan@tektutor:~$ <b>oc get svc</b>
<b>NAME    TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)    AGE</b>
nginx   ClusterIP   172.30.69.35   <none>        8081/TCP   3s
jegan@tektutor:~$ <b>oc describe svc/nginx</b>
Name:              nginx
Namespace:         jegan
Labels:            app=nginx
                   app.kubernetes.io/component=nginx
                   app.kubernetes.io/instance=nginx
Annotations:       <none>
Selector:          deployment=nginx
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                172.30.69.35
IPs:               172.30.69.35
Port:              <unset>  8081/TCP
TargetPort:        8081/TCP
Endpoints:         10.128.2.23:8081,10.128.2.26:8081,10.128.2.27:8081 + 2 more...
Session Affinity:  None
Events:            <none>
jegan@tektutor:~$ <b>oc run dnstest -it --restart Never --rm --image tutum/dnsutils bash</b>

If you don't see a command prompt, try pressing enter.

root@dnstest:/# root@dnstest:/# 
root@dnstest:/# 
root@dnstest:/# curl nginx:8081
<b>bash: curl: command not found</b>
root@dnstest:/# <b>apt update && apt install -y curl</b>
Ign http://archive.ubuntu.com trusty InRelease
Get:1 http://archive.ubuntu.com trusty-updates InRelease [65.9 kB]
Get:2 http://archive.ubuntu.com trusty-security InRelease [65.9 kB]
Get:3 http://archive.ubuntu.com trusty Release.gpg [933 B]
Get:4 http://archive.ubuntu.com trusty Release [58.5 kB]        
Get:5 http://archive.ubuntu.com trusty-updates/main Sources [532 kB]
Get:6 http://archive.ubuntu.com trusty-updates/restricted Sources [6444 B]     
Get:7 http://archive.ubuntu.com trusty-updates/universe Sources [288 kB]       
Get:8 http://archive.ubuntu.com trusty-updates/main amd64 Packages [1460 kB]   
Get:9 http://archive.ubuntu.com trusty-updates/restricted amd64 Packages [21.4 kB]
Get:10 http://archive.ubuntu.com trusty-updates/universe amd64 Packages [671 kB]
Get:11 http://archive.ubuntu.com trusty-security/main Sources [220 kB]         
Get:12 http://archive.ubuntu.com trusty-security/restricted Sources [5050 B]   
Get:13 http://archive.ubuntu.com trusty-security/universe Sources [127 kB]     
Get:14 http://archive.ubuntu.com trusty-security/main amd64 Packages [1032 kB] 
Get:15 http://archive.ubuntu.com trusty-security/restricted amd64 Packages [18.1 kB]
Get:16 http://archive.ubuntu.com trusty-security/universe amd64 Packages [378 kB]
Get:17 http://archive.ubuntu.com trusty/main Sources [1335 kB]                 
Get:18 http://archive.ubuntu.com trusty/restricted Sources [5335 B]            
Get:19 http://archive.ubuntu.com trusty/universe Sources [7926 kB]             
Get:20 http://archive.ubuntu.com trusty/main amd64 Packages [1743 kB]          
Get:21 http://archive.ubuntu.com trusty/restricted amd64 Packages [16.0 kB]    
Get:22 http://archive.ubuntu.com trusty/universe amd64 Packages [7589 kB]      
Fetched 23.6 MB in 14s (1608 kB/s)                                             
Reading package lists... Done
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following extra packages will be installed:
  ca-certificates libasn1-8-heimdal libcurl3 libgssapi3-heimdal
  libhcrypto4-heimdal libheimbase1-heimdal libheimntlm0-heimdal
  libhx509-5-heimdal libidn11 libkrb5-26-heimdal libldap-2.4-2
  libroken18-heimdal librtmp0 libsasl2-2 libsasl2-modules libsasl2-modules-db
  libwind0-heimdal openssl
Suggested packages:
  libsasl2-modules-otp libsasl2-modules-ldap libsasl2-modules-sql
  libsasl2-modules-gssapi-mit libsasl2-modules-gssapi-heimdal
The following NEW packages will be installed:
  ca-certificates curl libasn1-8-heimdal libcurl3 libgssapi3-heimdal
  libhcrypto4-heimdal libheimbase1-heimdal libheimntlm0-heimdal
  libhx509-5-heimdal libidn11 libkrb5-26-heimdal libldap-2.4-2
  libroken18-heimdal librtmp0 libsasl2-2 libsasl2-modules libsasl2-modules-db
  libwind0-heimdal openssl
0 upgraded, 19 newly installed, 0 to remove and 111 not upgraded.
Need to get 2152 kB of archives.
After this operation, 6868 kB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu/ trusty-updates/main libroken18-heimdal amd64 1.6~git20131207+dfsg-1ubuntu1.2 [39.9 kB]
Get:2 http://archive.ubuntu.com/ubuntu/ trusty-updates/main libasn1-8-heimdal amd64 1.6~git20131207+dfsg-1ubuntu1.2 [160 kB]
Get:3 http://archive.ubuntu.com/ubuntu/ trusty-updates/main libhcrypto4-heimdal amd64 1.6~git20131207+dfsg-1ubuntu1.2 [84.1 kB]
Get:4 http://archive.ubuntu.com/ubuntu/ trusty-updates/main libheimbase1-heimdal amd64 1.6~git20131207+dfsg-1ubuntu1.2 [29.0 kB]
Get:5 http://archive.ubuntu.com/ubuntu/ trusty-updates/main libwind0-heimdal amd64 1.6~git20131207+dfsg-1ubuntu1.2 [47.9 kB]
Get:6 http://archive.ubuntu.com/ubuntu/ trusty-updates/main libhx509-5-heimdal amd64 1.6~git20131207+dfsg-1ubuntu1.2 [104 kB]
Get:7 http://archive.ubuntu.com/ubuntu/ trusty-updates/main libkrb5-26-heimdal amd64 1.6~git20131207+dfsg-1ubuntu1.2 [196 kB]
Get:8 http://archive.ubuntu.com/ubuntu/ trusty-updates/main libheimntlm0-heimdal amd64 1.6~git20131207+dfsg-1ubuntu1.2 [15.2 kB]
Get:9 http://archive.ubuntu.com/ubuntu/ trusty-updates/main libgssapi3-heimdal amd64 1.6~git20131207+dfsg-1ubuntu1.2 [89.7 kB]
Get:10 http://archive.ubuntu.com/ubuntu/ trusty-updates/main libidn11 amd64 1.28-1ubuntu2.2 [94.6 kB]
Get:11 http://archive.ubuntu.com/ubuntu/ trusty/main libsasl2-modules-db amd64 2.1.25.dfsg1-17build1 [14.9 kB]
Get:12 http://archive.ubuntu.com/ubuntu/ trusty/main libsasl2-2 amd64 2.1.25.dfsg1-17build1 [56.5 kB]
Get:13 http://archive.ubuntu.com/ubuntu/ trusty-updates/main libldap-2.4-2 amd64 2.4.31-1+nmu2ubuntu8.5 [153 kB]
Get:14 http://archive.ubuntu.com/ubuntu/ trusty-updates/main librtmp0 amd64 2.4+20121230.gitdf6c518-1ubuntu0.1 [50.4 kB]
Get:15 http://archive.ubuntu.com/ubuntu/ trusty-updates/main libcurl3 amd64 7.35.0-1ubuntu2.20 [173 kB]
Get:16 http://archive.ubuntu.com/ubuntu/ trusty-updates/main openssl amd64 1.0.1f-1ubuntu2.27 [489 kB]
Get:17 http://archive.ubuntu.com/ubuntu/ trusty-updates/main ca-certificates all 20170717~14.04.2 [166 kB]
Get:18 http://archive.ubuntu.com/ubuntu/ trusty/main libsasl2-modules amd64 2.1.25.dfsg1-17build1 [64.3 kB]
Get:19 http://archive.ubuntu.com/ubuntu/ trusty-updates/main curl amd64 7.35.0-1ubuntu2.20 [123 kB]
Fetched 2152 kB in 6s (340 kB/s)                                               
Preconfiguring packages ...
Selecting previously unselected package libroken18-heimdal:amd64.
(Reading database ... 11700 files and directories currently installed.)
Preparing to unpack .../libroken18-heimdal_1.6~git20131207+dfsg-1ubuntu1.2_amd64.deb ...
Unpacking libroken18-heimdal:amd64 (1.6~git20131207+dfsg-1ubuntu1.2) ...
Selecting previously unselected package libasn1-8-heimdal:amd64.
Preparing to unpack .../libasn1-8-heimdal_1.6~git20131207+dfsg-1ubuntu1.2_amd64.deb ...
Unpacking libasn1-8-heimdal:amd64 (1.6~git20131207+dfsg-1ubuntu1.2) ...
Selecting previously unselected package libhcrypto4-heimdal:amd64.
Preparing to unpack .../libhcrypto4-heimdal_1.6~git20131207+dfsg-1ubuntu1.2_amd64.deb ...
Unpacking libhcrypto4-heimdal:amd64 (1.6~git20131207+dfsg-1ubuntu1.2) ...
Selecting previously unselected package libheimbase1-heimdal:amd64.
Preparing to unpack .../libheimbase1-heimdal_1.6~git20131207+dfsg-1ubuntu1.2_amd64.deb ...
Unpacking libheimbase1-heimdal:amd64 (1.6~git20131207+dfoc run dnstest -it --restart Never --rm --image tutum/dnsutils bashsg-1ubuntu1.2) ...
Selecting previously unselected package libwind0-heimdal:amd64.
Preparing to unpack .../libwind0-heimdal_1.6~git20131207+dfsg-1ubuntu1.2_amd64.deb ...
Unpacking libwind0-heimdal:amd64 (1.6~git20131207+dfsg-1ubuntu1.2) ...
Selecting previously unselected package libhx509-5-heimdal:amd64.
Preparing to unpack .../libhx509-5-heimdal_1.6~git20131207+dfsg-1ubuntu1.2_amd64.deb ...
Unpacking libhx509-5-heimdal:amd64 (1.6~git20131207+dfsg-1ubuntu1.2) ...
Selecting previously unselected package libkrb5-26-heimdal:amd64.
Preparing to unpack .../libkrb5-26-heimdal_1.6~git20131207+dfsg-1ubuntu1.2_amd64.deb ...
Unpacking libkrb5-26-heimdal:amd64 (1.6~git20131207+dfsg-1ubuntu1.2) ...
Selecting previously unselected package libheimntlm0-heimdal:amd64.
Preparing to unpack .../libheimntlm0-heimdal_1.6~git20131207+dfsg-1ubuntu1.2_amd64.deb ...
Unpacking libheimntlm0-heimdal:amd64 (1.6~git20131207+dfsg-1ubuntu1.2) ...
Selecting previously unselected package libgssapi3-heimdal:amd64.
Preparing to unpack .../libgssapi3-heimdal_1.6~git20131207+dfsg-1ubuntu1.2_amd64.deb ...
Unpacking libgssapi3-heimdal:amd64 (1.6~git20131207+dfsg-1ubuntu1.2) ...
Selecting previously unselected package libidn11:amd64.
Preparing to unpack .../libidn11_1.28-1ubuntu2.2_amd64.deb ...
Unpacking libidn11:amd64 (1.28-1ubuntu2.2) ...
Selecting previously unselected package libsasl2-modules-db:amd64.
Preparing to unpack .../libsasl2-modules-db_2.1.25.dfsg1-17build1_amd64.deb ...
Unpacking libsasl2-modules-db:amd64 (2.1.25.dfsg1-17build1) ...
Selecting previously unselected package libsasl2-2:amd64.
Preparing to unpack .../libsasl2-2_2.1.25.dfsg1-17build1_amd64.deb ...
Unpacking libsasl2-2:amd64 (2.1.25.dfsg1-17build1) ...
Selecting previously unselected package libldap-2.4-2:amd64.
Preparing to unpack .../libldap-2.4-2_2.4.31-1+nmu2ubuntu8.5_amd64.deb ...
Unpacking libldap-2.4-2:amd64 (2.4.31-1+nmu2ubuntu8.5) ...
Selecting previously unselected package librtmp0:amd64.
Preparing to unpack .../librtmp0_2.4+20121230.gitdf6c518-1ubuntu0.1_amd64.deb ...
Unpacking librtmp0:amd64 (2.4+20121230.gitdf6c518-1ubuntu0.1) ...
Selecting previously unselected package libcurl3:amd64.
Preparing to unpack .../libcurl3_7.35.0-1ubuntu2.20_amd64.deb ...
Unpacking libcurl3:amd64 (7.35.0-1ubuntu2.20) ...
Selecting previously unselected package openssl.
Preparing to unpack .../openssl_1.0.1f-1ubuntu2.27_amd64.deb ...
Unpacking openssl (1.0.1f-1ubuntu2.27) ...
Selecting previously unselected package ca-certificates.
Preparing to unpack .../ca-certificates_20170717~14.04.2_all.deb ...
Unpacking ca-certificates (20170717~14.04.2) ...
Selecting previously unselected package libsasl2-modules:amd64.
Preparing to unpack .../libsasl2-modules_2.1.25.dfsg1-17build1_amd64.deb ...
Unpacking libsasl2-modules:amd64 (2.1.25.dfsg1-17build1) ...
Selecting previously unselected package curl.
Preparing to unpack .../curl_7.35.0-1ubuntu2.20_amd64.deb ...
Unpacking curl (7.35.0-1ubuntu2.20) ...
Setting up libroken18-heimdal:amd64 (1.6~git20131207+dfsg-1ubuntu1.2) ...
Setting up libasn1-8-heimdal:amd64 (1.6~git20131207+dfsg-1ubuntu1.2) ...
Setting up libhcrypto4-heimdal:amd64 (1.6~git20131207+dfsg-1ubuntu1.2) ...
Setting up libheimbase1-heimdal:amd64 (1.6~git20131207+dfsg-1ubuntu1.2) ...
Setting up libwind0-heimdal:amd64 (1.6~git20131207+dfsg-1ubuntu1.2) ...
Setting up libhx509-5-heimdal:amd64 (1.6~git20131207+dfsg-1ubuntu1.2) ...
Setting up libkrb5-26-heimdal:amd64 (1.6~git20131207+dfsg-1ubuntu1.2) ...
Setting up libheimntlm0-heimdal:amd64 (1.6~git20131207+dfsg-1ubuntu1.2) ...
Setting up libgssapi3-heimdal:amd64 (1.6~git20131207+dfsg-1ubuntu1.2) ...
Setting up libidn11:amd64 (1.28-1ubuntu2.2) ...
Setting up libsasl2-modules-db:amd64 (2.1.25.dfsg1-17build1) ...
Setting up libsasl2-2:amd64 (2.1.25.dfsg1-17build1) ...
Setting up libldap-2.4-2:amd64 (2.4.31-1+nmu2ubuntu8.5) ...
Setting up librtmp0:amd64 (2.4+20121230.gitdf6c518-1ubuntu0.1) ...
Setting up libcurl3:amd64 (7.35.0-1ubuntu2.20) ...
Setting up openssl (1.0.1f-1ubuntu2.27) ...
Setting up ca-certificates (20170717~14.04.2) ...
Setting up libsasl2-modules:amd64 (2.1.25.dfsg1-17build1) ...
Setting up curl (7.35.0-1ubuntu2.20) ...
Processing triggers for libc-bin (2.19-0ubuntu6.6) ...
Processing triggers for ca-certificates (20170717~14.04.2) ...
Updating certificates in /etc/ssl/certs... 148 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d....done.
root@dnstest:/# <b>curl nginx:8081</b>
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
Welcome to nginx!
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
root@dnstest:/# exit
exit
pod "dnstest" deleted
jegan@tektutor:~$
</pre>

It is also possible to access any type of service within the OpenShift cluster with the Service IP and its port as shown below
```
curl 172.30.69.35:8081
curl http://172.30.69.35:8081
curl http://nginx:8081
```

The expected output is

<pre>
root@dnstest:/# <b>curl 172.30.69.35:8081</b>
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
Welcome to nginx!
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
</pre>

## ⛹️‍♂️ Lab - Let's delete the project to clean up all the deployments, services, routes, etc we created earlier
```
oc delete project jegan
```

The expected output is
<pre>
jegan@tektutor:~$ <b>oc delete project jegan</b>
project.project.openshift.io "jegan" deleted
</pre>


## ⛹️‍♀️ Lab - Let's create a new project to try the next lab exercise
```
oc new-project jegan
```
The expected output is

<pre>
jegan@tektutor:~$ <b>oc new-project jegan</b>
Already on project "jegan" on server "https://api.tektutor.tektutor.org:6443".

You can add applications to this project with the 'new-app' command. For example, try:

    oc new-app rails-postgresql-example

to build a new example application in Ruby. Or use kubectl to deploy a simple Kubernetes application:

    kubectl create deployment hello-node --image=k8s.gcr.io/serve_hostname
</pre>

Let's now try to deploy an simple spring boot based microservice application using a Dockerfile from GitHub Repository

```
oc new-app https://github.com/tektutor/spring-ms.git
```

To be precise, though the above GitHub repository has the source code of the SpringBoot application, OpenShift will pick the Dockerfile as the first choice from the above GitHub Repository by default.

Using the Dockerfile from the GitHub, it then builds the custom image and pushes the image into OpenShift Private Container Registry before it proceeds to deploy the application into the cluster.

The expected output is

<pre>
jegan@tektutor:~$ <b>oc new-app https://github.com/tektutor/spring-ms.git</b>
--> Found container image 15bbbf6 (7 days old) from docker.io for "docker.io/openjdk:latest"

    * An image stream tag will be created as "openjdk:latest" that will track the source image
    * A Docker build using source code from https://github.com/tektutor/spring-ms.git will be created
      * The resulting image will be pushed to image stream tag "spring-ms:latest"
      * Every time "openjdk:latest" changes a new build will be triggered

--> Creating resources ...
    imagestream.image.openshift.io "openjdk" created
    imagestream.image.openshift.io "spring-ms" created
    buildconfig.build.openshift.io "spring-ms" created
    deployment.apps "spring-ms" created
--> Success
    Build scheduled, use 'oc logs -f buildconfig/spring-ms' to track its progress.
    Run 'oc status' to view your app.
</pre>

You may check the status at any point in time
```
oc status
```

The expected output is
<pre>
jegan@tektutor:~$ <b>oc status</b>
In project jegan on server https://api.tektutor.tektutor.org:6443

deployment/spring-ms deploys istag/spring-ms:latest <-
  bc/spring-ms docker builds https://github.com/tektutor/spring-ms.git on istag/openjdk:latest 
    not built yet
  deployment #1 running for 3 seconds - 0/1 pods growing to 1


2 warnings, 1 info identified, use 'oc status --suggest' to see details.
</pre>

Let's now check, the build
```
oc get builds
oc get bc time -o json
```

Let us now check, how many pods are running
```
oc get po -w
```

The expected output is
<pre>
jegan@tektutor:~/tekton$ <b>oc get po -w</b>
<b>NAME                READY   STATUS     RESTARTS   AGE</b>
spring-ms-1-build   0/1     Init:0/2   0          7s
spring-ms-1-build   0/1     Init:1/2   0          8s
spring-ms-1-build   0/1     PodInitializing   0          9s
spring-ms-1-build   1/1     Running           0          10s
spring-ms-6f5669c487-7hh94   0/1     Pending           0          0s
spring-ms-6f5669c487-7hh94   0/1     Pending           0          0s
spring-ms-6f5669c487-7hh94   0/1     ContainerCreating   0          0s
spring-ms-1-build            0/1     Completed           0          49s
spring-ms-6f5669c487-7hh94   0/1     ContainerCreating   0          3s
spring-ms-6f5669c487-7hh94   1/1     Running             0          14s
</pre>

Java spring-boot applications typically uses port 8080, hence let's create a clusterip service for the above deployment.

```
oc expose deploy/spring-ms --port=8080
oc describe svc/spring-ms
```

The expected output is
<pre>
jegan@tektutor:~$ <b>oc expose deploy spring-ms --port=8080</b>
service/spring-ms exposed
jegan@tektutor:~$ <b>oc describe svc/spring-ms</b>
Name:              spring-ms
Namespace:         jegan
Labels:            app=spring-ms
                   app.kubernetes.io/component=spring-ms
                   app.kubernetes.io/instance=spring-ms
Annotations:       <none>
Selector:          deployment=spring-ms
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                172.30.223.200
IPs:               172.30.223.200
Port:              <unset>  8080/TCP
TargetPort:        8080/TCP
Endpoints:         10.128.2.114:8080
Session Affinity:  None
Events:            <none>
</pre>

Let's create a public route for the service to access the service from outside the OpenShift cluster

If you don't mention the type of service while creating, OpenShift assumes you wish to create a CluterIP internal service.
```
oc expose svc spring-ms
```

The expected output is

<pre>
jegan@tektutor:~$ <b>oc expose svc spring-ms</b>
route.route.openshift.io/spring-ms exposed
</pre>

Let's us now list the route
```
oc get route
```

The expected output is
<pre>
jegan@tektutor:~$ <b>oc get route</b>
<b>NAME        HOST/PORT                                    PATH   SERVICES    PORT   TERMINATION   WILDCARD</b>
spring-ms   spring-ms-jegan.apps.tektutor.tektutor.org          spring-ms   8080                 None
</pre>

Let's us now find details about the route

```
oc describe route spring-ms
```

The expected output is

<pre>
jegan@tektutor:~$ oc describe route spring-ms
Name:			spring-ms
Namespace:		jegan
Created:		5 minutes ago
Labels:			app=spring-ms
			app.kubernetes.io/component=spring-ms
			app.kubernetes.io/instance=spring-ms
Annotations:		openshift.io/host.generated=true
Requested Host:		spring-ms-jegan.apps.tektutor.tektutor.org
			   exposed on router default (host router-default.apps.tektutor.tektutor.org) 5 minutes ago
Path:			<none>
TLS Termination:	<none>
Insecure Policy:	<none>
Endpoint Port:		8080

Service:	spring-ms
Weight:		100 (100%)
Endpoints:	10.128.2.114:8080
</pre>

You may now access the route as shown below

```
curl spring-ms-jegan.apps.tektutor.tektutor.org
```

The expected output is
<pre>
jegan@tektutor:~$ <b>curl spring-ms-jegan.apps.tektutor.tektutor.org</b>
Greetings from Spring Boot!
</pre>

## ⛹️‍♂️ Lab - Understanding a multi-pod application deployment using Wordpress and Mariadb database
```
oc delete project jegan
oc new-project jegan
oc new-app mariadb-ephemeral
oc new-app php~https://github.com/wordpress/wordpress
oc logs -f dc/wordpress
oc expose svc/wordpress
oc get routes
```

## ⛹️‍♀️ Lab - Understanding blue-green deployment in OpenShift

Create the blue deployment and expose a route as shown below

```
oc new-project jegan-bluegreen --display-name="Blue Green Project" --description="Demonstrates Blue Green Deployment in OCP v4.9"
oc new-app --image-stream=php --code=https://github.com/RedHatWorkshops/bluegreen --env COLOR=blue --name=blue
oc get builds
oc logs build/blue-1
oc get pods
oc get service
oc get route
oc expose service blue --name=bluegreen
oc get route
```

Now create a green deployment of the same application

```
oc new-app --image-stream=php --code=https://github.com/RedHatWorkshops/bluegreen --env COLOR=green --name=green
oc get service
```

Edit the route to forward traffic to green

```
oc edit route bluegreen
```

Change the service name from blue to green and save it.

Test the route
```
oc get route
```

## ⛹️‍♂️ Lab - Understanding A/B Testing 
```
oc delete project jegan-bluegreen
oc new-project ab-deployment --display-name="A/B Deployment" --description="Demonstrates A/B Test Deployment Strategy in OCP."
oc new-app openshift/deployment-example --name=ab-example-a
oc new-app openshift/deployment-example:v2 --name=ab-example-b
oc expose svc/ab-example-a
oc get route
```

Now let's test the route and see which version of the application is live in the Cluster
```
curl ab-example-a-jegan-ab-deployment.apps.tektutor.tektutor.org
```

Let us scale the deployments
```
oc get deploy
oc scale deploy ab-example-a --replicas=2
oc scale deploy ab-example-b --replicas=2
oc get pods
```

Now let's edit the existing route
```
oc edit route ab-example-a
```

The expected output will be similar to
<pre>
  1 # Please edit the object below. Lines beginning with a '#' will be ignored,
  2 # and an empty file will abort the edit. If an error occurs while saving this file will be
  3 # reopened with the relevant failures.
  4 #
  5 apiVersion: route.openshift.io/v1
  6 kind: Route
  7 metadata:
  8   annotations:
  9     openshift.io/host.generated: "true"
 10   creationTimestamp: "2022-02-21T02:20:28Z"
 11   labels:
 12     app: ab-example-a
 13     app.kubernetes.io/component: ab-example-a
 14     app.kubernetes.io/instance: ab-example-a
 15   name: ab-example-a
 16   namespace: jegan-ab-deployment
 17   resourceVersion: "122224"
 18   uid: 620f826f-944f-4dde-9766-4e0d4fa58b25
 19 spec:
 20   <b>alternateBackends:
 21   - kind: Service
 22     name: ab-example-b
 23     weight: 50</b>
 24   host: ab-example-a-jegan-ab-deployment.apps.tektutor.tektutor.org
 25   port:
 26     targetPort: 8080-tcp
 27   to:
 28     kind: Service
 29     name: ab-example-a
 30     weight: 50
 31   wildcardPolicy: None
 32 status:
 33   ingress:
 34   - conditions:
 35     - lastTransitionTime: "2022-02-21T02:20:28Z"
 36       status: "True"
 37       type: Admitted
 38     host: ab-example-a-jegan-ab-deployment.apps.tektutor.tektutor.org
 39     routerCanonicalHostname: router-default.apps.tektutor.tektutor.org
 40     routerName: default
 41     wildcardPolicy: None
</pre>

Make sure you saved it before exiting.

Now try to access the route repeatedly as much time as possible to notice the traffic gets routed to different deployment version.
```
curl ab-example-a-jegan-ab-deployment.apps.tektutor.tektutor.org
curl ab-example-a-jegan-ab-deployment.apps.tektutor.tektutor.org
curl ab-example-a-jegan-ab-deployment.apps.tektutor.tektutor.org
curl ab-example-a-jegan-ab-deployment.apps.tektutor.tektutor.org
```

## ⛹️‍♀️ Lab - Creating a deployment in declarative style

Let us clean any existing project and its deployments, pods, etc.,
```
oc delete jegan
```
You need to replace your project name in the place of "jegan" above

```
cd ~
git clone https://github.com/tektutor/openshift-tekton-feb-2022.git
cd Day2/declarative-manifests
openshift-tekton-feb-2022
oc new-project jegan
oc apply -f spring-ms-deploy.yml
```
The expected output is
<pre>
jegan@tektutor:~/tekton/Day2/declarative-manifests$ <b>oc apply -f spring-ms-deploy.yml</b>
deployment.apps/spring-ms created
</pre>

See if the deployment is created
```
oc get deploy
```
The expected output is
<pre>
jegan@tektutor:~/tekton/Day2/declarative-manifests$ <b>oc get deploy</b>
<b>NAME        READY   UP-TO-DATE   AVAILABLE   AGE</b>
spring-ms   1/1     1            1           3s
</pre>

Now let's create a NodePort external service for the above deployment in declarative style
```
oc apply -f spring-ms-nodeport-svc.yml 
```

The expected output is

<pre>
jegan@tektutor:~/tekton/Day2/declarative-manifests$ <b>oc apply -f spring-ms-nodeport-svc.yml</b>
service/spring-ms created
</pre>

Let us now list and see if the service is created

```
oc get svc
```
spring-ms-nodeport-svc.yml
The expected output is
<pre>
egan@tektutor:~/tekton/Day2/declarative-manifests$ <b>oc get svc</b>
<b>NAME        TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE</b>
spring-ms   NodePort   172.30.51.83   <none>        8080:30085/TCP   2s
</pre>

## ⛹️‍♂️ Lab - Creating a ClusterIP Internal Service in declarative style

Let's us first delete the existing service(if any)
```
oc get svc
```
The expected output is
<pre>
jegan@tektutor:~/tekton/Day2/declarative-manifests$ <b>oc get svc</b>
<b>NAME        TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE</b>
spring-ms   NodePort   172.30.51.83   <none>        8080:30085/TCP   2s
</pre>

Let's now delete that service
```
cd ~
cd openshift-tekton-feb-2022
git pull
cd Day2/declarative-manifests
oc delete -f spring-ms-nodeport-svc.yml
```
The expected output is
<pre>
jegan@tektutor:~/tekton/Day2/declarative-manifests$ <b>oc delete -f spring-ms-nodeport-svc.yml</b>
service "spring-ms" deleted
</pre>

Now it is time to create the ClusterIP Internal service declaratively

```
cd ~
cd openshift-tekton-feb-2022
git pull
cd Day2/declarative-manifests
oc apply -f spring-ms-clusterip-svc.yml
oc get svc
oc describe svc/spring-ms
```

The expected output is

<pre>
jegan@tektutor:~/tekton/Day2/declarative-manifests$ <b>oc apply -f spring-ms-clusterip-svc.yml</b>
service/spring-ms created
jegan@tektutor:~/tekton/Day2/declarative-manifests$ <b>oc get svc</b>
<b>NAME        TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE</b>
spring-ms   ClusterIP   172.30.81.216   <none>        8080/TCP   4s
jegan@tektutor:~/tekton/Day2/declarative-manifests$ <b>oc describe svc/spring-ms</b>
Name:              spring-ms
Namespace:         jegan
Labels:            app=spring-ms
Annotations:       <none>
Selector:          deployment=spring-ms
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                172.30.81.216
IPs:               172.30.81.216
Port:              <unset>  8080/TCP
TargetPort:        8080/TCP
Endpoints:         10.128.3.19:8080
Session Affinity:  None
Events:            <none>
</pre>

## ⛹️‍♂️ Lab - Creating a LoadBalancer External Service in declarative style

Let's us first delete the existing service(if any)
```
oc get svc
```
The expected output is
<pre>
jegan@tektutor:~/tekton/Day2/declarative-manifests$ <b>oc get svc</b>
<b>NAME        TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE</b>
spring-ms   ClusterIP   172.30.81.216   <none>        8080/TCP   4s
</pre>

Let's now delete that service
```
cd ~
cd openshift-tekton-feb-2022
git pull
cd Day2/declarative-manifests
oc delete -f spring-ms-clusterip-svc.yml
```
The expected output is
<pre>
egan@tektutor:~/tekton/Day2/declarative-manifests$ oc delete -f spring-ms-clusterip-svc.yml 
service "spring-ms" deleted
</pre>

Now it is time to create the Loadbalancer External service declaratively

```
cd ~
cd openshift-tekton-feb-2022
git pull
cd Day2/declarative-manifests
oc apply -f spring-ms-loadbalancer-svc.yml 
oc get svc
oc describe svc/spring-ms
```

The expected output is

<pre>
jegan@tektutor:~/tekton/Day2/declarative-manifests$ <b>oc apply -f spring-ms-loadbalancer-svc.yml</b>
service/spring-ms created
jegan@tektutor:~/tekton/Day2/declarative-manifests$ <b>oc get svc</b>
NAME        TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
spring-ms   LoadBalancer   172.30.215.214   <pending>     8080:31301/TCP   2s
jegan@tektutor:~/tekton/Day2/declarative-manifests$ <b>oc describe svc/spring-ms</b>
Name:                     spring-ms
Namespace:                jegan
Labels:                   app=spring-ms
Annotations:              <none>
Selector:                 deployment=spring-ms
Type:                     LoadBalancer
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       172.30.215.214
IPs:                      172.30.215.214
Port:                     <unset>  8080/TCP
TargetPort:               8080/TCP
NodePort:                 <unset>  31301/TCP
Endpoints:                10.128.3.19:8080
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
</pre>

## What is a Custom Resource in Kubernetes/OpenShift ?
- an API extension mechanism in Kubernetes/OpenShift
- helps you add a new kind of object in your OpenShift Cluster just like Deployment, ReplicaSet, Pod, etc.,
- a Custom Resource Definition(CRD) defines a Custom Resource(CR)
- once a CR is created using CRD it can be accessed using kubectl or oc commands

## What is an Operator in Kubernetes/OpenShift?
- an Operator is a custom Kubernetes/OpenShift Controller that waches a CR
- the custom application level controllers monitors CR 
- Custom Controllers monitors CR compares its desired with actual state, if it deviates takes appropriate actions
- Operators can help in 
    - scaling up/down a CR
    - upgrading a CR from one version to another
    - helps infrasturce engineers & developers who would like to extend Kubernetes API to manage their site and software

## What is Operator SDK?
- builds on top of Kuberenetes controller-runtime libraries 
- provides essential Kubernetes controller runtimes in Go programming lanaguage
- a set of tools that helps in developing, building and deploying an Operator into Kubernetes/OpenShift

## What is Operator Lifecycle Manager (OLM) ?
- it takes the Operator pattern one level above by creating a OLM Operator which manages Operators
- it lets you define Operators declaratively

## What is Operator Metering?
- is used to analyze the resource usage of Operators running in Kubernetes/OpenShift
- CPU Usage, memory usage, and other metrics





