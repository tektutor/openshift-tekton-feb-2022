### Login to OpenShift Cluster using CLI client
```
oc login -u kubeadmin https://api.tektutor.okd4.tektutor.org:6443
```
The expected output is
<pre>
oc login -u kubeadmin https://api.tektutor.tektutor.org:6443
Authentication required for https://api.tektutor.tektutor.org:6443 (openshift)
Username: kubeadmin
Password: 
Login successful.

You have access to 65 projects, the list has been suppressed. You can list all projects with 'oc projects'
</pre>

### Listing the nodes in your OpenShift Cluster
```
jegan@tektutor:~$ oc get nodes
```

The expected output is

<pre>
NAME                             STATUS   ROLES           AGE   VERSION
master-1.tektutor.tektutor.org   Ready    master,worker   62m   v1.22.3+fdba464
master-2.tektutor.tektutor.org   Ready    master,worker   63m   v1.22.3+fdba464
master-3.tektutor.tektutor.org   Ready    master,worker   63m   v1.22.3+fdba464
worker-1.tektutor.tektutor.org   Ready    worker          44m   v1.22.3+fdba464
worker-2.tektutor.tektutor.org   Ready    worker          45m   v1.22.3+fdba464
</pre>

### List Openshift Nodes with IP details
```
oc get nodes -o wide
```

The expected output is

<pre>
jegan@tektutor:~$ <b>oc get nodes -o wide</b>
NAME                             STATUS   ROLES           AGE   VERSION           INTERNAL-IP       EXTERNAL-IP   OS-IMAGE                                                       KERNEL-VERSION                 CONTAINER-RUNTIME
master-1.tektutor.tektutor.org   Ready    master,worker   64m   v1.22.3+fdba464   192.168.122.13    <none>        Red Hat Enterprise Linux CoreOS 49.84.202202081504-0 (Ootpa)   4.18.0-305.34.2.el8_4.x86_64   cri-o://1.22.1-14.rhaos4.9.git7486bc8.el8
master-2.tektutor.tektutor.org   Ready    master,worker   65m   v1.22.3+fdba464   192.168.122.228   <none>        Red Hat Enterprise Linux CoreOS 49.84.202202081504-0 (Ootpa)   4.18.0-305.34.2.el8_4.x86_64   cri-o://1.22.1-14.rhaos4.9.git7486bc8.el8
master-3.tektutor.tektutor.org   Ready    master,worker   64m   v1.22.3+fdba464   192.168.122.89    <none>        Red Hat Enterprise Linux CoreOS 49.84.202202081504-0 (Ootpa)   4.18.0-305.34.2.el8_4.x86_64   cri-o://1.22.1-14.rhaos4.9.git7486bc8.el8
worker-1.tektutor.tektutor.org   Ready    worker          46m   v1.22.3+fdba464   192.168.122.36    <none>        Red Hat Enterprise Linux CoreOS 49.84.202202081504-0 (Ootpa)   4.18.0-305.34.2.el8_4.x86_64   cri-o://1.22.1-14.rhaos4.9.git7486bc8.el8
worker-2.tektutor.tektutor.org   Ready    worker          47m   v1.22.3+fdba464   192.168.122.222   <none>        Red Hat Enterprise Linux CoreOS 49.84.202202081504-0 (Ootpa)   4.18.0-305.34.2.el8_4.x86_64   cri-o://1.22.1-14.rhaos4.9.git7486bc8.el8
</pre>

### Find more details of an OpenShift Cluster Node
```
oc describe node/master-1.tektutor.tektutor.org
```

The expected output will be similar to

<pre>
jegan@tektutor:~$ <b>oc describe node master-1.tektutor.tektutor.org</b>
Name:               master-1.tektutor.tektutor.org
Roles:              master,worker
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=master-1.tektutor.tektutor.org
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/master=
                    node-role.kubernetes.io/worker=
                    node.openshift.io/os_id=rhcos
Annotations:        machineconfiguration.openshift.io/controlPlaneTopology: HighlyAvailable
                    machineconfiguration.openshift.io/currentConfig: rendered-master-f79e2d3db5844af0fd9d3f0f28e56004
                    machineconfiguration.openshift.io/desiredConfig: rendered-master-f79e2d3db5844af0fd9d3f0f28e56004
                    machineconfiguration.openshift.io/reason: 
                    machineconfiguration.openshift.io/state: Done
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Fri, 18 Feb 2022 17:34:13 +0530
Taints:             <none>
Unschedulable:      false
Lease:
  HolderIdentity:  master-1.tektutor.tektutor.org
  AcquireTime:     <unset>
  RenewTime:       Fri, 18 Feb 2022 18:41:28 +0530
Conditions:
  Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----             ------  -----------------                 ------------------                ------                       -------
  MemoryPressure   False   Fri, 18 Feb 2022 18:38:58 +0530   Fri, 18 Feb 2022 17:34:13 +0530   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure     False   Fri, 18 Feb 2022 18:38:58 +0530   Fri, 18 Feb 2022 17:34:13 +0530   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure      False   Fri, 18 Feb 2022 18:38:58 +0530   Fri, 18 Feb 2022 17:34:13 +0530   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready            True    Fri, 18 Feb 2022 18:38:58 +0530   Fri, 18 Feb 2022 17:37:13 +0530   KubeletReady                 kubelet is posting ready status
Addresses:
  InternalIP:  192.168.122.13
  Hostname:    master-1.tektutor.tektutor.org
Capacity:
  cpu:                8
  ephemeral-storage:  104322028Ki
  hugepages-1Gi:      0
  hugepages-2Mi:      0
  memory:             16408472Ki
  pods:               250
Allocatable:
  cpu:                7500m
  ephemeral-storage:  96143180846
  hugepages-1Gi:      0
  hugepages-2Mi:      0
  memory:             15257496Ki
  pods:               250
System Info:
  Machine ID:                             c7815dc9cb4647008c7ebd238ae33d7e
  System UUID:                            c7815dc9-cb46-4700-8c7e-bd238ae33d7e
  Boot ID:                                d001b987-4a3e-4bea-8e71-8ec04c8f7569
  Kernel Version:                         4.18.0-305.34.2.el8_4.x86_64
  OS Image:                               Red Hat Enterprise Linux CoreOS 49.84.202202081504-0 (Ootpa)
  Operating System:                       linux
  Architecture:                           amd64
  Container Runtime Version:              cri-o://1.22.1-14.rhaos4.9.git7486bc8.el8
  Kubelet Version:                        v1.22.3+fdba464
  Kube-Proxy Version:                     v1.22.3+fdba464
Non-terminated Pods:                      (40 in total)
  Namespace                               Name                                                       CPU Requests  CPU Limits  Memory Requests  Memory Limits  Age
  ---------                               ----                                                       ------------  ----------  ---------------  -------------  ---
  openshift-apiserver                     apiserver-7fdc47455d-cpcf8                                 110m (1%)     0 (0%)      250Mi (1%)       0 (0%)         54m
  openshift-authentication                oauth-openshift-6cbb4fc67c-6sz7f                           10m (0%)      0 (0%)      50Mi (0%)        0 (0%)         55m
  openshift-cluster-node-tuning-operator  tuned-xgt5f                                                10m (0%)      0 (0%)      50Mi (0%)        0 (0%)         62m
  openshift-cluster-samples-operator      cluster-samples-operator-76d94fcc49-zczxx                  20m (0%)      0 (0%)      100Mi (0%)       0 (0%)         61m
  openshift-console                       downloads-7f9bf9b68c-lzjxn                                 10m (0%)      0 (0%)      50Mi (0%)        0 (0%)         55m
  openshift-controller-manager            controller-manager-jxtsj                                   100m (1%)     0 (0%)      100Mi (0%)       0 (0%)         54m
  openshift-dns                           dns-default-zqfbc                                          60m (0%)      0 (0%)      110Mi (0%)       0 (0%)         62m
  openshift-dns                           node-resolver-szrtr                                        5m (0%)       0 (0%)      21Mi (0%)        0 (0%)         62m
  openshift-etcd                          etcd-master-1.tektutor.tektutor.org                        400m (5%)     0 (0%)      930Mi (6%)       0 (0%)         55m
  openshift-etcd                          etcd-quorum-guard-5749966797-76v4m                         10m (0%)      0 (0%)      5Mi (0%)         0 (0%)         65m
  openshift-image-registry                image-registry-5d984d476-7x9sx                             100m (1%)     0 (0%)      256Mi (1%)       0 (0%)         55m
  openshift-image-registry                node-ca-hf62g                                              10m (0%)      0 (0%)      10Mi (0%)        0 (0%)         55m
  openshift-ingress-canary                ingress-canary-n78cn                                       10m (0%)      0 (0%)      20Mi (0%)        0 (0%)         56m
  openshift-ingress                       router-default-7bcf88769f-fgjhw                            100m (1%)     0 (0%)      256Mi (1%)       0 (0%)         56m
  openshift-kube-apiserver                kube-apiserver-master-1.tektutor.tektutor.org              290m (3%)     0 (0%)      1224Mi (8%)      0 (0%)         54m
  openshift-kube-controller-manager       kube-controller-manager-master-1.tektutor.tektutor.org     80m (1%)      0 (0%)      500Mi (3%)       0 (0%)         50m
  openshift-kube-scheduler                openshift-kube-scheduler-master-1.tektutor.tektutor.org    25m (0%)      0 (0%)      150Mi (1%)       0 (0%)         55m
  openshift-machine-config-operator       machine-config-controller-7c7d749bd-lvzhm                  20m (0%)      0 (0%)      50Mi (0%)        0 (0%)         62m
  openshift-machine-config-operator       machine-config-daemon-f8cdh                                40m (0%)      0 (0%)      100Mi (0%)       0 (0%)         66m
  openshift-machine-config-operator       machine-config-server-slvtm                                20m (0%)      0 (0%)      50Mi (0%)        0 (0%)         62m
  openshift-marketplace                   certified-operators-zxprg                                  10m (0%)      0 (0%)      50Mi (0%)        0 (0%)         62m
  openshift-marketplace                   community-operators-hnrst                                  10m (0%)      0 (0%)      50Mi (0%)        0 (0%)         62m
  openshift-marketplace                   redhat-marketplace-2jrcb                                   10m (0%)      0 (0%)      50Mi (0%)        0 (0%)         62m
  openshift-marketplace                   redhat-operators-dnv5f                                     10m (0%)      0 (0%)      50Mi (0%)        0 (0%)         62m
  openshift-monitoring                    alertmanager-main-1                                        8m (0%)       0 (0%)      105Mi (0%)       0 (0%)         55m
  openshift-monitoring                    grafana-6bd6749c8c-btt85                                   5m (0%)       0 (0%)      84Mi (0%)        0 (0%)         55m
  openshift-monitoring                    kube-state-metrics-df96cc89f-s9j4m                         4m (0%)       0 (0%)      110Mi (0%)       0 (0%)         63m
  openshift-monitoring                    node-exporter-bm76j                                        9m (0%)       0 (0%)      47Mi (0%)        0 (0%)         63m
  openshift-monitoring                    openshift-state-metrics-6cf8b69947-l8mgh                   3m (0%)       0 (0%)      72Mi (0%)        0 (0%)         63m
  openshift-monitoring                    prometheus-k8s-0                                           100m (1%)     0 (0%)      1119Mi (7%)      0 (0%)         55m
  openshift-monitoring                    telemeter-client-8dfc7b475-l766r                           3m (0%)       0 (0%)      70Mi (0%)        0 (0%)         63m
  openshift-multus                        multus-additional-cni-plugins-kzppw                        10m (0%)      0 (0%)      10Mi (0%)        0 (0%)         67m
  openshift-multus                        multus-admission-controller-jxl9w                          20m (0%)      0 (0%)      70Mi (0%)        0 (0%)         64m
  openshift-multus                        multus-x8bfw                                               10m (0%)      0 (0%)      65Mi (0%)        0 (0%)         67m
  openshift-multus                        network-metrics-daemon-ck7b5                               20m (0%)      0 (0%)      120Mi (0%)       0 (0%)         67m
  openshift-network-diagnostics           network-check-target-8gj5w                                 10m (0%)      0 (0%)      15Mi (0%)        0 (0%)         67m
  openshift-oauth-apiserver               apiserver-ffdbf84c9-r6jfm                                  150m (2%)     0 (0%)      200Mi (1%)       0 (0%)         63m
  openshift-operator-lifecycle-manager    packageserver-5ccbc9cbbb-xdjsz                             10m (0%)      0 (0%)      50Mi (0%)        0 (0%)         64m
  openshift-sdn                           sdn-controller-5k72z                                       10m (0%)      0 (0%)      50Mi (0%)        0 (0%)         67m
  openshift-sdn                           sdn-mhk4x                                                  110m (1%)     0 (0%)      220Mi (1%)       0 (0%)         67m
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests      Limits
  --------           --------      ------
  cpu                1952m (26%)   0 (0%)
  memory             6889Mi (46%)  0 (0%)
  ephemeral-storage  0 (0%)        0 (0%)
  hugepages-1Gi      0 (0%)        0 (0%)
  hugepages-2Mi      0 (0%)        0 (0%)
Events:              <none>
</pre>

### Print node usage statistics
```
oc adm top nodes
```

The expected output is

<pre>
jegan@tektutor:~$ <b>oc adm top nodes</b>
NAME                             CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%   
master-1.tektutor.tektutor.org   1782m        23%    7618Mi          51%       
master-2.tektutor.tektutor.org   1730m        23%    7356Mi          49%       
master-3.tektutor.tektutor.org   1920m        25%    6831Mi          45%       
worker-1.tektutor.tektutor.org   280m         5%     1221Mi          8%        
worker-2.tektutor.tektutor.org   234m         4%     1210Mi          8%        
</pre>

### Removing worker role from master node
Before removing the worker role from master nodes
<pre>
jegan@tektutor:~$ <b>oc get nodes</b>
NAME                             STATUS   ROLES           AGE   VERSION
master-1.tektutor.tektutor.org   Ready    master,worker   62m   v1.22.3+fdba464
master-2.tektutor.tektutor.org   Ready    master,worker   63m   v1.22.3+fdba464
master-3.tektutor.tektutor.org   Ready    master,worker   63m   v1.22.3+fdba464
worker-1.tektutor.tektutor.org   Ready    worker          44m   v1.22.3+fdba464
worker-2.tektutor.tektutor.org   Ready    worker          45m   v1.22.3+fdba464
</pre>

Let's remove the worker role from the master nodes

```
oc patch schedulers.config.openshift.io/cluster --type merge -p '{"spec":{"mastersSchedulable":false}}'
```

After removing the worker role from master nodes
<pre>
jegan@tektutor:~$ <b>oc patch schedulers.config.openshift.io/cluster --type merge -p '{"spec":{"mastersSchedulable":false}}'</b>
scheduler.config.openshift.io/cluster patched
jegan@tektutor:~$ <b>oc get nodes</b>
NAME                             STATUS   ROLES    AGE   VERSION
master-1.tektutor.tektutor.org   Ready    master   86m   v1.22.3+fdba464
master-2.tektutor.tektutor.org   Ready    master   88m   v1.22.3+fdba464
master-3.tektutor.tektutor.org   Ready    master   87m   v1.22.3+fdba464
worker-1.tektutor.tektutor.org   Ready    worker   68m   v1.22.3+fdba464
worker-2.tektutor.tektutor.org   Ready    worker   69m   v1.22.3+fdba464
</pre>

### Adding worker role to the master nodes
Before adding the worker role to the master nodes

<pre>
jegan@tektutor:~$ <b>oc get nodes</b>
NAME                             STATUS   ROLES    AGE   VERSION
master-1.tektutor.tektutor.org   Ready    master   86m   v1.22.3+fdba464
master-2.tektutor.tektutor.org   Ready    master   88m   v1.22.3+fdba464
master-3.tektutor.tektutor.org   Ready    master   87m   v1.22.3+fdba464
worker-1.tektutor.tektutor.org   Ready    worker   68m   v1.22.3+fdba464
worker-2.tektutor.tektutor.org   Ready    worker   69m   v1.22.3+fdba464
</pre>

Now let's add the worker role to all the master nodes in the OpenShift cluster

```
oc patch schedulers.config.openshift.io/cluster --type merge -p '{"spec":{"mastersSchedulable":true}}'
```

After adding the worker role to the master nodes

<pre>
jegan@tektutor:~$ oc patch schedulers.config.openshift.io/cluster --type merge -p '{"spec":{"mastersSchedulable":true}}'
scheduler.config.openshift.io/cluster patched
jegan@tektutor:~$ oc get nodes
NAME                             STATUS   ROLES           AGE   VERSION
master-1.tektutor.tektutor.org   Ready    master,worker   91m   v1.22.3+fdba464
master-2.tektutor.tektutor.org   Ready    master,worker   92m   v1.22.3+fdba464
master-3.tektutor.tektutor.org   Ready    master,worker   91m   v1.22.3+fdba464
worker-1.tektutor.tektutor.org   Ready    worker          73m   v1.22.3+fdba464
worker-2.tektutor.tektutor.org   Ready    worker          74m   v1.22.3+fdba464
</pre>

### Listing the existing projects in OpenShift cluster
```
oc get projects
```

The expected output is

<pre>
jegan@tektutor:~$ oc get projects
NAME                                               DISPLAY NAME   STATUS
default                                                           Active
kube-node-lease                                                   Active
kube-public                                                       Active
kube-system                                                       Active
openshift                                                         Active
openshift-apiserver                                               Active
openshift-apiserver-operator                                      Active
openshift-authentication                                          Active
openshift-authentication-operator                                 Active
openshift-cloud-controller-manager                                Active
openshift-cloud-controller-manager-operator                       Active
openshift-cloud-credential-operator                               Active
openshift-cluster-csi-drivers                                     Active
openshift-cluster-machine-approver                                Active
openshift-cluster-node-tuning-operator                            Active
openshift-cluster-samples-operator                                Active
openshift-cluster-storage-operator                                Active
openshift-cluster-version                                         Active
openshift-config                                                  Active
openshift-config-managed                                          Active
openshift-config-operator                                         Active
openshift-console                                                 Active
openshift-console-operator                                        Active
openshift-console-user-settings                                   Active
openshift-controller-manager                                      Active
openshift-controller-manager-operator                             Active
openshift-dns                                                     Active
openshift-dns-operator                                            Active
openshift-etcd                                                    Active
openshift-etcd-operator                                           Active
openshift-host-network                                            Active
openshift-image-registry                                          Active
openshift-infra                                                   Active
openshift-ingress                                                 Active
openshift-ingress-canary                                          Active
openshift-ingress-operator                                        Active
openshift-insights                                                Active
openshift-kni-infra                                               Active
openshift-kube-apiserver                                          Active
openshift-kube-apiserver-operator                                 Active
openshift-kube-controller-manager                                 Active
openshift-kube-controller-manager-operator                        Active
openshift-kube-scheduler                                          Active
openshift-kube-scheduler-operator                                 Active
openshift-kube-storage-version-migrator                           Active
openshift-kube-storage-version-migrator-operator                  Active
openshift-kubevirt-infra                                          Active
openshift-machine-api                                             Active
openshift-machine-config-operator                                 Active
openshift-marketplace                                             Active
openshift-monitoring                                              Active
openshift-multus                                                  Active
openshift-network-diagnostics                                     Active
openshift-network-operator                                        Active
openshift-node                                                    Active
openshift-oauth-apiserver                                         Active
openshift-openstack-infra                                         Active
openshift-operator-lifecycle-manager                              Active
openshift-operators                                               Active
openshift-ovirt-infra                                             Active
openshift-sdn                                                     Active
openshift-service-ca                                              Active
openshift-service-ca-operator                                     Active
openshift-user-workload-monitoring                                Active
openshift-vsphere-infra                                           Active
</pre>

### Creating a project from command line

Though using your name as project name is neither professional nor a best practice. For this training, I
would suggest use your name as 10 participants are sharing a single OpenShift cluster.  Using your name
as project name, helps other participants using the same cluster to identify the projects they created
vs other participants.

This also helps unintented deletion of projects created by other participants.

```
oc new-project jegan
```

The expected output is
<pre>
jegan@tektutor:~$ oc new-project jegan
Already on project "jegan" on server "https://api.tektutor.tektutor.org:6443".

You can add applications to this project with the 'new-app' command. For example, try:

    oc new-app rails-postgresql-example

to build a new example application in Ruby. Or use kubectl to deploy a simple Kubernetes application:

    kubectl create deployment hello-node --image=k8s.gcr.io/serve_hostname
</pre>


### Creating an application
```
oc new-app twalter/openshift-nginx:stable --name nginx
```

The expected output is
<pre>
jegan@tektutor:~$ <b>oc new-app twalter/openshift-nginx:stable --name nginx</b>
--> Found container image 4786608 (3 years old) from Docker Hub for "twalter/openshift-nginx:stable"

    * An image stream tag will be created as "nginx:stable" that will track this image

--> Creating resources ...
    imagestream.image.openshift.io "nginx" created
    deployment.apps "nginx" created
    service "nginx" created
--> Success
    Application is not exposed. You can expose services to the outside world by executing one or more of the commands below:
     'oc expose service/nginx' 
    Run 'oc status' to view your app.
</pre>

Let's check the status of the deployments as shown below

```
oc status
```

The expected output is

<pre>
egan@tektutor:~$ <b>oc status</b>
In project jegan on server https://api.tektutor.tektutor.org:6443

svc/nginx - 172.30.155.175 ports 80, 8081
  deployment/nginx deploys istag/nginx:stable 
    deployment #2 running for 47 seconds - 1 pod
    deployment #1 deployed 52 seconds ago


1 info identified, use 'oc status --suggest' to see details.
</pre>

### List the deployments under your project

```
oc get deploy
```

The expected output is
<pre>
jegan@tektutor:~$ oc get deploy
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
nginx   1/1     1            1           97s
</pre>

### List the replicasets under your project

```
oc get rs
```

The expected output is
<pre>
jegan@tektutor:~$ oc get rs
NAME               DESIRED   CURRENT   READY   AGE
nginx-5dd56f5c87   1         1         1       96s
nginx-6f99d9668b   0         0         0       101s
</pre>


### List the pods in your project

```
oc get po
```

The expected output is

<pre>
jegan@tektutor:~$ oc get po
NAME                     READY   STATUS    RESTARTS   AGE
nginx-5dd56f5c87-qg9vv   1/1     Running   0          99s
</pre>


### Find details of a pod 

```
oc describe pod nginx-5dd56f5c87-qg9vv
```

The expected output is

<pre>
jegan@tektutor:~$ <b>oc describe pod nginx-5dd56f5c87-qg9vv</b>
Name:         nginx-5dd56f5c87-qg9vv
Namespace:    jegan
Priority:     0
Node:         worker-1.tektutor.tektutor.org/192.168.122.36
Start Time:   Fri, 18 Feb 2022 19:11:47 +0530
Labels:       deployment=nginx
              pod-template-hash=5dd56f5c87
Annotations:  k8s.v1.cni.cncf.io/network-status:
                [{
                    "name": "openshift-sdn",
                    "interface": "eth0",
                    "ips": [
                        "10.128.2.23"
                    ],
                    "default": true,
                    "dns": {}
                }]
              k8s.v1.cni.cncf.io/networks-status:
                [{
                    "name": "openshift-sdn",
                    "interface": "eth0",
                    "ips": [
                        "10.128.2.23"
                    ],
                    "default": true,
                    "dns": {}
                }]
              openshift.io/generated-by: OpenShiftNewApp
              openshift.io/scc: restricted
Status:       Running
IP:           10.128.2.23
IPs:
  IP:           10.128.2.23
Controlled By:  ReplicaSet/nginx-5dd56f5c87
Containers:
  nginx:
    Container ID:   cri-o://3ce51e0eda9606f88f8ae256c18f8e9655e33a96569b5311370e165276ba83e9
    Image:          twalter/openshift-nginx@sha256:b6a09b124c14ea2bb81f6081fb0d6e4f5214b9a1c98f6173fffc8e07d2382ca3
    Image ID:       docker.io/twalter/openshift-nginx@sha256:b6a09b124c14ea2bb81f6081fb0d6e4f5214b9a1c98f6173fffc8e07d2382ca3
    Ports:          80/TCP, 8081/TCP
    Host Ports:     0/TCP, 0/TCP
    State:          Running
      Started:      Fri, 18 Feb 2022 19:11:50 +0530
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-sflcd (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  kube-api-access-sflcd:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
    ConfigMapName:           openshift-service-ca.crt
    ConfigMapOptional:       <nil>
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason          Age    From               Message
  ----    ------          ----   ----               -------
  Normal  Scheduled       5m10s  default-scheduler  Successfully assigned jegan/nginx-5dd56f5c87-qg9vv to worker-1.tektutor.tektutor.org
  Normal  AddedInterface  5m7s   multus             Add eth0 [10.128.2.23/23] from openshift-sdn
  Normal  Pulled          5m7s   kubelet            Container image "twalter/openshift-nginx@sha256:b6a09b124c14ea2bb81f6081fb0d6e4f5214b9a1c98f6173fffc8e07d2382ca3" already present on machine
  Normal  Created         5m7s   kubelet            Created container nginx
  Normal  Started         5m7s   kubelet            Started container nginx
</pre>

### Find details of a replicaset
```
oc describe rs/nginx-5dd56f5c87
```

The expected output is

<pre>
jegan@tektutor:~$ <b>oc describe rs/nginx-5dd56f5c87</b>
Name:           nginx-5dd56f5c87
Namespace:      jegan
Selector:       deployment=nginx,pod-template-hash=5dd56f5c87
Labels:         deployment=nginx
                pod-template-hash=5dd56f5c87
Annotations:    deployment.kubernetes.io/desired-replicas: 1
                deployment.kubernetes.io/max-replicas: 2
                deployment.kubernetes.io/revision: 2
                image.openshift.io/triggers:
                  [{"from":{"kind":"ImageStreamTag","name":"nginx:stable"},"fieldPath":"spec.template.spec.containers[?(@.name==\"nginx\")].image"}]
                openshift.io/generated-by: OpenShiftNewApp
Controlled By:  Deployment/nginx
Replicas:       1 current / 1 desired
Pods Status:    1 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:       deployment=nginx
                pod-template-hash=5dd56f5c87
  Annotations:  openshift.io/generated-by: OpenShiftNewApp
  Containers:
   nginx:
    Image:        twalter/openshift-nginx@sha256:b6a09b124c14ea2bb81f6081fb0d6e4f5214b9a1c98f6173fffc8e07d2382ca3
    Ports:        80/TCP, 8081/TCP
    Host Ports:   0/TCP, 0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:
  Type    Reason            Age    From                   Message
  ----    ------            ----   ----                   -------
  Normal  SuccessfulCreate  8m30s  replicaset-controller  Created pod: nginx-5dd56f5c87-qg9vv
</pre>

### Finding more details of a deployment
```
oc describe deploy/nginx
```

The expected output is

<pre>jegan@tektutor:~$ <b>oc get deploy</b>
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
nginx   1/1     1            1           12m
jegan@tektutor:~$ <b>oc describe deploy/nginx</b>
Name:                   nginx
Namespace:              jegan
CreationTimestamp:      Fri, 18 Feb 2022 19:11:42 +0530
Labels:                 app=nginx
                        app.kubernetes.io/component=nginx
                        app.kubernetes.io/instance=nginx
Annotations:            deployment.kubernetes.io/revision: 2
                        image.openshift.io/triggers:
                          [{"from":{"kind":"ImageStreamTag","name":"nginx:stable"},"fieldPath":"spec.template.spec.containers[?(@.name==\"nginx\")].image"}]
                        openshift.io/generated-by: OpenShiftNewApp
Selector:               deployment=nginx
Replicas:               1 desired | 1 updated | 1 total | 1 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:       deployment=nginx
  Annotations:  openshift.io/generated-by: OpenShiftNewApp
  Containers:
   nginx:
    Image:        twalter/openshift-nginx@sha256:b6a09b124c14ea2bb81f6081fb0d6e4f5214b9a1c98f6173fffc8e07d2382ca3
    Ports:        80/TCP, 8081/TCP
    Host Ports:   0/TCP, 0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   nginx-5dd56f5c87 (1/1 replicas created)
Events:
  Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
  Normal  ScalingReplicaSet  12m   deployment-controller  Scaled up replica set nginx-6f99d9668b to 1
  Normal  ScalingReplicaSet  12m   deployment-controller  Scaled up replica set nginx-5dd56f5c87 to 1
  Normal  ScalingReplicaSet  12m   deployment-controller  Scaled down replica set nginx-6f99d9668b to 0
</pre>

### Scaling up a deployment
```
oc scale deploy nginx --replicas=5
```

The expected output is
<pre>
jegan@tektutor:~$ <b>oc get deploy</b>
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
nginx   1/1     1            1           14m
jegan@tektutor:~$ <b>oc scale deploy nginx --replicas=5</b>
deployment.apps/nginx scaled
jegan@tektutor:~$ <b>oc get po</b>
NAME                     READY   STATUS              RESTARTS   AGE
nginx-5dd56f5c87-4jq5q   0/1     ContainerCreating   0          3s
nginx-5dd56f5c87-qg9vv   1/1     Running             0          14m
nginx-5dd56f5c87-sg57k   1/1     Running             0          3s
nginx-5dd56f5c87-sv8bj   0/1     ContainerCreating   0          3s
nginx-5dd56f5c87-zb5cw   1/1     Running             0          3s
jegan@tektutor:~$ <b>oc get po -w</b>
NAME                     READY   STATUS    RESTARTS   AGE
nginx-5dd56f5c87-4jq5q   1/1     Running   0          6s
nginx-5dd56f5c87-qg9vv   1/1     Running   0          14m
nginx-5dd56f5c87-sg57k   1/1     Running   0          6s
nginx-5dd56f5c87-sv8bj   1/1     Running   0          6s
nginx-5dd56f5c87-zb5cw   1/1     Running   0          6s
</pre>

### Creating a NodePort external service for nginx deployment

```
oc expose deploy/nginx --type=NodePort --port=80
```

The expected output is

<pre>
jegan@tektutor:~$ <b>oc expose deploy/nginx --type=NodePort --port=80</b>
service/nginx exposed
jegan@tektutor:~$ <b>oc get svc</b>
NAME    TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
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
Endpoints:                10.128.2.23:80,10.128.2.26:80,10.128.2.27:80 + 2 more...
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
</pre>
