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
jegan@tektutor:~$ oc get nodes -o wide
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
jegan@tektutor:~$ oc describe node master-1.tektutor.tektutor.org
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
```
oc new-project jegan
```

Though using your name as project name is neither professional nor a best practice. For this training, I
would suggest use your name as 10 participants are sharing a single OpenShift cluster.  Using your name
as project name, helps other participants using the same cluster to identify the projects they created
vs other participants.

This also helps unintented deletion of projects created by other participants.

### Creating an application
```
oc new-app twalter/openshift-nginx:stable --name nginx
```

You can check the status of the deployments as shown below

```
oc status
```

