# Day 1 - RedHat OpenShift Container Platform (OCP)
For training/consulting/coaching, you may reach me

<pre>
    jegan@tektutor.org
    +91 822-000-5626 (WhatsApp)
</pre>

## ⛔ Need your attention - You don't have to install OpenShift in our Training Lab
<pre>
- Our training lab environment already has OpenShift Cluster pre-installed
- Hence, you don't have to perform any installation listed below
- The installation procedures listed below are meant for your future reference
- Any attempt to perform OpenShift installation in our lab environment will corrupt our OpenShift cluster
</pre>

## 🔴🔴 Do and Don'ts, please don't get offended ⛔⛔
<pre>
- Kindly stick to the credential details given to you.  
- Please avoid switching from one user to other user. 
- Please avoid switching between the clusters.
- Please create only one project per participant as the Cluster is shared by 10 participants.
- Please use your name as the project name so we can easily manage them.
- At any point in time, please do not scale beyond 5 pods per participants, imagine 5 x 20 participants = 100 Pods.
  Once you are done with a lab exercise, please delete the project and recreate with the same name.
</pre>

## What will happen if I don't follow the above requests :question::question::question:
<pre>
- When you switch using other user credentials, actually you will end up using other participant's lab machine.  
- It will be confusing for both of you, as the projects gets switched in your lab everytime other participant 
  switches to his/her project and vice versa on other participants lab environment. 
- There is a chance that either you or the other participant may delete each other projects.
- It will overload our cluster leading to many of our deployments crashing. 
- This might even bring down our cluster altogether. 
- We will lose lot of time in fixing the cluster.
</pre>

🧑‍🤝‍🧑 Hence your kind co-operation is requested to deliver this training smoothly.

## ℹ️ OpenShift Installation Options
1. RedHat OpenShift Code Ready Containers (CRC) - Ideal for self-learning purposes only 🎓👨‍🎓👩‍🎓
2. RedHat OpenShift Developer Sandbox - Ideal for self-learning purposes only 🎓👨‍🎓👩‍🎓
3. Installer Provisioned Infrastructure (IPI) - Ideal for R&D 🚀🛰️ , Development 🕵️‍♀️🕵️‍ and Production ⛈️⛅🌕
4. User Provisioned Infrastructure (UPI) - Ideal for Learning 👨‍🎓👨‍🎓👩‍, R&D 🚀🚀, Development 🕵️‍♀️🕵️‍ & Production ⛈️⛅🌕

## ℹ️ Installing RedHat OpenShift Code Ready Containers (CRC)
:x: Please don't attempt this in our training lab as this may corrupt our OpenShift cluster.  The instructions are captured here for your future reference, i.e in case you wish to try this at home post the training.

This will create a virtual machine using KVM and minimal openshift components are installed within the virtual machine. You need to make sure nested VM is enabled before installing CRC.

The cluster will have a single node that supports both master and worker roles.

##### ℹ️ Installing kubectl
:x: Please do not try this in our lab environment as it will corrupt our OpenShift cluster installation.  These instructions are here to help you in setting up OpenShift in your personal laptop/desktop post the training for your self-learning purposes only.

```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x ./kubectl
sudo mv ./kubectl /usr/bin
```
When prompted for password, type administrator password of your Linux OS.

##### ℹ️ Installing Code Ready Containers in Linux
:x: Please do not try this in our lab environment as it will corrupt our OpenShift cluster installation.  These instructions are here to help you in setting up OpenShift in your personal laptop/desktop post the training for your self-learning purposes only.

```
cd /home/alchemy/Downloads
tar xvf crc-linux-amd64.tar.xz
cd crc-linux-1.38.0-amd64
./crc setup
```

The expected output is
<pre>
jegan@ubuntu:~/Downloads/crc-linux-1.38.0-amd64$ <b>./crc setup</b>
INFO Checking if running as non-root              
INFO Checking if running inside WSL2              
INFO Checking if crc-admin-helper executable is cached 
INFO Checking for obsolete admin-helper executable 
INFO Checking if running on a supported CPU architecture 
INFO Checking minimum RAM requirements            
INFO Checking if crc executable symlink exists    
INFO Checking if Virtualization is enabled        
INFO Checking if KVM is enabled                   
INFO Checking if libvirt is installed             
INFO Checking if user is part of libvirt group    
INFO Checking if active user/process is currently part of the libvirt group 
INFO Checking if libvirt daemon is running        
INFO Checking if a supported libvirt version is installed 
INFO Checking if crc-driver-libvirt is installed  
INFO Installing crc-driver-libvirt                expose
INFO Checking crc daemon systemd service          
INFO Setting up crc daemon systemd service        
INFO Checking crc daemon systemd socket units     
INFO Setting up crc daemon systemd socket units   
INFO Checking if AppArmor is configured           
INFO Updating AppArmor configuration              
INFO Using root access: Updating AppArmor configuration 
[sudo] password for jegan: 
INFO Using root access: Changing permissions for /etc/apparmor.d/libvirt/TEMPLATE.qemu to 644  
INFO Checking if systemd-networkd is running      
INFO Checking if NetworkManager is installed      
INFO Checking if NetworkManager service is running 
INFO Checking if dnsmasq configurations file exist for NetworkManager 
INFO Checking if the systemd-resolved service is running 
INFO Checking if /etc/NetworkManager/dispatcher.d/99-crc.sh exists 
INFO Writing NetworkManager dispatcher file for crc 
INFO Using root access: Writing NetworkManager configuration to /etc/NetworkManager/dispatcher.d/99-crc.sh 
INFO Using root access: Changing permissions for /etc/NetworkManager/dispatcher.d/99-crc.sh to 755  
INFO Using root access: Executing systemctl daemon-reload command 
INFO Using root access: Executing systemctl reload NetworkManager 
INFO Checking if libvirt 'crc' network is available 
INFO Setting up libvirt 'crc' network             
INFO Checking if libvirt 'crc' network is active  
INFO Starting libvirt 'crc' network               
INFO Checking if CRC bundle is extracted in '$HOME/.crc' 
INFO Checking if /home/jegan/.crc/cache/crc_libvirt_4.9.12.crcbundle exists 
INFO Extracting bundle from the CRC executable    
INFO Ensuring directory /home/jegan/.crc/cache exists 
INFO Extracting embedded bundle crc_libvirt_4.9.12.crcbu:moneybag:ndle to /home/jegan/.crc/cache 
INFO Uncompressing crc_libvirt_4.9.12.crcbundle   
crc.qcow2: 11.69 GiB / 11.69 GiB [------------------------------------------------------] 100.00%
oc: 117.16 MiB / 117.16 MiB [-----------------------------------------------------------] 100.00%
Your system is correctly setup for using CodeReady Containers, you can now run 'crc start' to start the OpenShift cluster
</pre>

##### ℹ️ Starting your local CRC OpenShift Cluster
:x:  Please don't attempt this in our training lab.

```
./crc start
```
The expected output is
<pre>
[jegan@tektutor crc-linux-1.38.0-amd64]$ <b>./crc start</b>
INFO Checking if running as non-root              
INFO Checking if running inside WSL2              
INFO Checking if crc-admin-helper executable is cached 
INFO Checking for obsolete admin-helper executable 
INFO Checking if running on a supported CPU architecture 
INFO Checking minimum RAM requirements            
INFO Checking if crc executable symlink exists    
INFO Checking if Virtualization is enabled        
INFO Checking if KVM is enabled                   
INFO Checking if libvirt is installed             
INFO Checking if user is part of libvirt group    
INFO Checking if active user/process is currently part of the libvirt group 
INFO Checking if libvirt daemon is running        
INFO Checking if a supported libvirt version is installed 
INFO Checking if crc-driver-libvirt is installed  
INFO Checking crc daemon systemd socket units     
INFO Checking if systemd-networkd is running      
INFO Checking if NetworkManager is installed      
INFO Checking if NetworkManager service is running 
INFO Checking if /etc/NetworkManager/conf.d/crc-nm-dnsmasq.conf exists 
INFO Checking if /etc/NetworkManager/dnsmasq.d/crc.conf exists 
INFO Checking if libvirt 'crc' network is available 
INFO Checking if libvirt 'crc' network is active  
INFO Starting CodeReady Containers VM for OpenShift 4.9.12... 
INFO CodeReady Containers instance is running with IP 192.168.130.11 
INFO CodeReady Containers VM is running           
INFO Check internal and public DNS query...       
INFO Check DNS query from host...                 
INFO Verifying validity of the kubelet certificates... 
INFO Starting OpenShift kubelet service           
INFO Waiting for kube-apiserver availability... [takes around 2min] 
INFO Waiting for user's pull secret part of instance disk... 
INFO Starting OpenShift cluster... [waiting for the cluster to stabilize] 
INFO All operators are available. Ensuring stability... 
INFO Operators are stable (2/3)...                
INFO Operators are stable (3/3)...                
INFO Adding crc-admin and crc-developer contexts to kubeconfig... 
Started the OpenShift cluster.
penShift Installer Provisioned Ins
The server is accessible via web console at:
  https://console-openshift-console.apps-crc.testing

Log in as administrator:
  Username: kubeadmin
  Password: B8XxM-aY9yz-zhwJY-5HU7d

Log in as user:expose
  Username: developer
  Password: developer

Use the 'oc' command line interface:
  $ eval $(crc oc-env)
  $ oc login -u developer https://api.crc.testing:6443
[jegan@tektutor crc-linux-1.38.0-amd64]$ 
</pre>
when the crc prompts for pull secret, you need to paste the content of pull-secret.txt and hit enter.

##### ℹ️ Troubleshooting CRC start
:x:  Please don't attempt this in our training lab.

It is commonly noticed that ./crc start command fails many times. 

Make sure

1. Virtualization is enabled (VT-X/AMD-V)
2. You have sufficient RAM in the system atleast 16GB or more
3. You have alteast 8 vCPU in your system

Try to stop and startAgreement

```
./crc stop
./crc start
```

##### ℹ️ Login to CRC Cluster as a developer via CLI
:x:  Please don't attempt this in our training lab.

```
eval $(./crc oc-env)
oc login -u developer https://api.crc.testing:6443
```

##### ℹ️ Login to CRC Cluster as an administrator via CLI
:x:  Please don't attempt this in our training lab.

```
eval $(./crc oc-env)
oc login -u kubeadmin https://api.crc.testing:6443
```

## ℹ️ Using RedHat OpenShift Developer Sandbox for Free 👨‍🎓

🔴🔴🔴 As we already have a working OpenShift Cluster pre-installed, you don't have to do this during the training.🔴🔴🔴

You may setup a RedHat Cluster almost instantaneously and very helpful for self-learning.  However, some advanced features like Eventing, installing Operators, etc will not work in this Free environment.

https://developers.redhat.com/developer-sandbox?source=sso

## ℹ️ OpenShift Installer Provisioned Infrastructure (IPI) 💲💲💲
---
This mode of OpenShift installation is preferred if budget is not a constraint and you wish to perform the OpenShift installation in Cloud environments or with VMWare vSphere, etc.,

However, this style of Openshift installation offers less flexibility or configuration options but the installation efforts will be less, as pretty much the installer automates creating infrastructure (VMs, Network, OS installation, etc) and end-to-end OpenShift installation procedure.

### ℹ️ Story time - my personal experience
I recently installed RedHat OpenShift in AWS. 

I used the OpenShift cluster for 9 days

The automatic installation spinned off 

On Demand Linux Amazon Elastic Compute Cloud running Linux/Unix costed - $420
- EC2 m5.xlarge Instance ( 4 vCPU with 16 GB RAM ) 
- EC2 r5.xlarge Instance ( 4 vCPU with 32 GB RAM - good for memory intensive computing )
- EC2 m5.2xlarge ( 8 vCPU with 32 GB RAM )

Amazon NAT Gateway costed $94 
Load Balancing - $20 

The total bill was :heavy_dollar_sign::heavy_dollar_sign: $707(rounded) :angry: including :disappointed: :disappointed: GST $107.83 for 9 Days. This is way too expensive for your learning purpose, this is more suitable for :heavy_check_mark: corporates :moneybag: :heavy_dollar_sign: i.e Development :heavy_check_mark: & Production :heavy_check_mark:.

 :-1: Not recommended for self-learning

You may refer more details about this in the official documentation
https://docs.openshift.com/container-platform/4.9/installing/index.html

## :heavy_check_mark: OpenShift User Provisioned Infrastructure (UPI)
This mode of OpenShift installation is highly preferred :thumbsup: and flexible :satisfied: in many cases. This approach let's you take control of the installation process, allows you to customize things giving more flexibily in setting up your OpenShift in your own preferred way. 

But this involves doing everything manually yourself :weary: .  This is a very lengthy process and many things can go wrong during the installation, hence installing OpenShift using this approach involves several attempts but the end result almost always will be fruitful as you would have learned many things along the way :v:

I remember the first time I attempted this it took about 7 days :tired_face: to get my cluster up and running. The official documentations are very exhaustive and no single approach works in all environment, hence there are always many missing pieces of information without which things won't work in your environment. You need to find your solution for the puzzle all by yourself.  Sometimes it takes few minutes, few hours and sometimes it takes few days to find out the missing piece of information. It is like solving a puzzle. But once you have figured out what works in your environment, you can do the setup within 1 hour.

## ℹ️ Understanding our Training Lab OpenShift Setup
Our Training Lab is setup using User Provisioned Infrastructure, almost everything was performed manually.

Lab Server Hardware Configuration
<pre>
Dell PowerEdge R630 
Processor Type: Intel(R) Xeon(R) CPU E5-2683 v4 @ 2.10Ghz
  - Logical Processors: 64
NICs : 4
512 GB RAM
6 TB HDD
</pre>
The Server with this kind of configuration might cost you Rs.10,00,000+ 

We have used two such servers to setup our Lab with two OpenShift Clusters.

You may refer the official documentation for detailed installation instructions 
https://docs.openshift.com/container-platform/4.9/installing/index.html

- RedHat CentOS 7.9 64-bit OS is installed on the Server directly as base OS.
- Within RedHat CentOS 7.9, KVM Opensource Hypervisor is installed for Virtualization
- Using KVM ( Kernal-based Virtual Machine ) 6 Virtual Machines were created within RedHat CentOS v7.9
     - 3 master virtual machines are created to setup the OpenShift cluster with 3 Master Nodes
     - 2 worker Virtual machines are created to setup the OpenShift cluster with 2 Worker Nodes
     - 1 LoadBalancer virtual machines with HAProxy is setup to make the cluster accessible.  

- Master Node Virtual Machine Hardware Configuration (RedHat Enterprise Linux Core OS - v49.84.202202081504-0 [Ootpa])
  - 8 Virtual Cores
  - 64 GB RAM
  - 500 GB HDD Storage

- Worker Node Virtual Machine Hardware Configuration (RedHat Enterprise Linux Core OS - v49.84.202202081504-0[Ootpa])
  - 8 Virtual Cores
  - 64 GB RAM
  - 500 GB HDD Storage

- LoadBalancer (HAProxy - Centos 7 cloud image: CentOS-7-x86_64-GenericCloud.qcow2)
  - 2 Virtual Cores
  - 16 GB RAM
  - 100 GB HDD Storage

<pre>
As part of RedHat Enterprise Core OS, we get kubelet and CRI-O container runtime out of the box on all master and worker nodes.
Our OpenShift version is 4.9.21 which uses Kubernetes v1.22.3.x
There are 2 such separate OpenShift clusters setup for our training lab.

Each OpenShift cluster supports upto 10 users.
OpenShift Cluster - 1 ( 8 Users )
   - Server 1 ( 192.168.1.137 )
OpenShift Cluster - 2 ( 8 users )
   - Server 2 ( 192.168.1.138 )
</pre>

## RedHat OpenShift Container Platform v4.9 Architecture
1. kubectl create deploy nginx --image=nginx:latest
2. kubectl makes a REST call to API server with above information given in kubectl command
3. API server creates a Deployment object in etcd datastore
4. Deployment Controller receives the event that there is a new Deployment created in the Cluster
5. Deployment Controller request API Server to create ReplicaSet based on the information it received from the event
6. API Server creates a new ReplicaSet in etcd based on the request it received from Deployment Controller
7. This then trigger another event saying there is a new ReplicaSet that is created in the Cluster
8. ReplicaSet Controller receives a notification and then it will request the API Server to create Pod entries in etcd
9. API Server creates as many Pod entries requested by ReplicaSet Controller in the etcd datastore
10. New Pod entries created in etcd trigger new Pod created events in the cluster
11. Scheduler receives the New Pod created event and decides where these Pod containers can be scheduled and informs its decision to the API Server
12. API Server then updates the Pod definition which already there in the etcd store with the Node information recommended by Scheduler
13. This triggers another event, the kubelet Kubernetes Agent running on the respective nodes gets an event notification.
14. Kubelet checks if the container image required to create the Pod containers are present in its local container registry.  If it understands that the image required is missing, kubelet pulls the image from the respective image registry and then it creates the Pod containers.
15. Kubelet actually interacts with Container Runtime installed on the Node to get the image pulled, creating containers, etc.,
16. kubelet then updates the API Server periodically as a heart-beat update

Kubernetes Overview
Master Node
 Kubernetes Control Plane Components  
  - API Server
      - implements all Kubernetes functionalities as REST API
  - Scheduler
      - is responsible for identifying a health node where a Pod can be deployed
  - etcd
  - Controller Managers
      - Deployment Controller
      - Node Controller
      - Endpoint Controller
      - ReplicaSet Controller
 
- Container Runtime ( Docker, LXC, CRI-O, etc., )
- kubelet Kubernetes Agent
- kube-proxy
    - provides load-balancing functionality to the sevices
- CoreDNS
    - helps in supporting service discovery 
    - i.e it let's you access a service by its name as opposed to its IP Address

Woker Node
  - Container Runtime ( Docker, LXC, CRI-O,etc., )
  - kubelet Kubernetes Agent
  - kube-proxy
  - User Application Pods (if any)

Control Plane Components typically run in Master Node

OpenShift Overview
 - is RedHat's distribution of Kubernetes with many additional features developed on top of Kubernetes
 - Cluster is a collection of computers called nodes
 - Nodes can be Physical Servers, Virtual Machines or Compute Machines in Cloud (AWS,GCP,Azure,etc.,)
 - Basic unit of work that can be replicated is called a Pod
 - Pod is a group of related containers that shares network, storage and shared memory
 - The OpenShift cluster has two types of Nodes.
   1. Master Node 
     - Starting from RedHat OCP v4.2, the one and only supported OS is RedHat Enterprise Core OS
   2. Worker Node
     - This can be RedHat Enterprise Linux or RedHat Enterprise Core OS
 - OpenShift supports two types of planes
   1. Control Plane and
   2. Application Plane
 - Control Plane is nothing but Master node with its Componets, in other words Openshift itself
 - Application Plane or Data Plane is where user applications are deployed
 - Openshift uses CRI-O Container Engine.

Kubernetes/OpenShift Operators
  - its a convenient way you can package your application
      	  - easily deploy them in K8s or OpenShift cluster
      	  - udpate or upgrade them
      	  - remove them 
  - it comes with custom application level controllers
  - the appolication level controllers monitor your custom application and take action when certain things happen
  - Custom Controllers are created using CRD (Custom Resource Definition)
  - Through CRD you can create a Custom Resource

Master Node/Machine
 - Control Plane components runs here
      - OpenShift API Server
      - OpenShift etcd
      - OpenShift Scheduler
      - OpenShift Controller Managers
        - runs control loops that contanstly compare desired state of an application with actual state 
          and takes action in case they are different
      - OpenShift OAuth API Server
      	- responsible for managing user,group authentications
      - OpenShift OAuth Server
        - responsible for managing user request tokens
      - OpenShift DNS
      - Openshift Network Operator
 - kubelet - Kubernetes Node Agent
 
Worker Node/Machine
 - aka Compute Machines
 - User applications are deployed as Pods
 - kubelet Agent

Generally, Master Node doesn't allow deploying user applications. However, they can be configured to accept user applications in some special cases.

Command-line Client Tools
  oc 
  kubectl
  
RHCOS (RedHat Enterprise Core OS)
 - Operating System that is suitable for Container Orchestration Platform like RedHat OpenShift Container Platform
 - immutable Operating System
 - self updating OS
 - specially customized OS for containers
 - comes with CRI-O Container Engine and kubelet out of the box
 - ignition
     - during the first boot,it requires certain kernel configuration parameters that helps the RHCOS bootstrap the node
     - the ignition files are hosted in the LoadBalancer,hence it picks it during the first boot to configure itself 
       and gets connected to the cluster

## ⛹️‍♂️ Lab - Login to OpenShift Cluster using CLI client
```
oc login -u kubeadmin https://api.tektutor.okd4.tektutor.org:6443
```
The URL for your cluster will be different, hence check your Linux Desktop for a file named openshift.txt to find your API endpoint URL.

The expected output is
<pre>
oc login -u kubeadmin https://api.tektutor.tektutor.org:6443
Authentication required for https://api.tektutor.tektutor.org:6443 (openshift)
Username: kubeadmin
Password: 
Login successful.

You have access to 65 projects, the list has been suppressed. You can list all projects with 'oc projects'
</pre>

## ⛹️‍♀️ Lab - Listing the nodes in your OpenShift Cluster
```
jegan@tektutor:~$ <b>oc get nodes</b>
```

The expected output is

<pre>
<b>NAME                             STATUS   ROLES           AGE   VERSION</b>
master-1.tektutor.tektutor.org   Ready    master,worker   62m   v1.22.3+fdba464
master-2.tektutor.tektutor.org   Ready    master,worker   63m   v1.22.3+fdba464
master-3.tektutor.tektutor.org   Ready    master,worker   63m   v1.22.3+fdba464
worker-1.tektutor.tektutor.org   Ready    worker          44m   v1.22.3+fdba464
worker-2.tektutor.tektutor.org   Ready    worker          45m   v1.22.3+fdba464
</pre>

## ⛹️‍♂️ Lab - List Openshift Nodes with IP details
```
oc get nodes -o wide
```

The expected output is

<pre>
jegan@tektutor:~$ <b>oc get nodes -o wide</b>
<b>NAME                             STATUS   ROLES           AGE   VERSION           INTERNAL-IP       EXTERNAL-IP   OS-IMAGE                                                       KERNEL-VERSION                 CONTAINER-RUNTIME</b>
master-1.tektutor.tektutor.org   Ready    master,worker   64m   v1.22.3+fdba464   192.168.122.13    <none>        Red Hat Enterprise Linux CoreOS 49.84.202202081504-0 (Ootpa)   4.18.0-305.34.2.el8_4.x86_64   cri-o://1.22.1-14.rhaos4.9.git7486bc8.el8
master-2.tektutor.tektutor.org   Ready    master,worker   65m   v1.22.3+fdba464   192.168.122.228   <none>        Red Hat Enterprise Linux CoreOS 49.84.202202081504-0 (Ootpa)   4.18.0-305.34.2.el8_4.x86_64   cri-o://1.22.1-14.rhaos4.9.git7486bc8.el8
master-3.tektutor.tektutor.org   Ready    master,worker   64m   v1.22.3+fdba464   192.168.122.89    <none>        Red Hat Enterprise Linux CoreOS 49.84.202202081504-0 (Ootpa)   4.18.0-305.34.2.el8_4.x86_64   cri-o://1.22.1-14.rhaos4.9.git7486bc8.el8
worker-1.tektutor.tektutor.org   Ready    worker          46m   v1.22.3+fdba464   192.168.122.36    <none>        Red Hat Enterprise Linux CoreOS 49.84.202202081504-0 (Ootpa)   4.18.0-305.34.2.el8_4.x86_64   cri-o://1.22.1-14.rhaos4.9.git7486bc8.el8
worker-2.tektutor.tektutor.org   Ready    worker          47m   v1.22.3+fdba464   192.168.122.222   <none>        Red Hat Enterprise Linux CoreOS 49.84.202202081504-0 (Ootpa)   4.18.0-305.34.2.el8_4.x86_64   cri-o://1.22.1-14.rhaos4.9.git7486bc8.el8
</pre>

## ⛹️‍♂️ Lab - Find more details of an OpenShift Cluster Node
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
  HolderIdentity:  master-1.tektutor.tektutor.org:heavy_dollar_sign:
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

## ⛹️‍ Lab - Print node usage statistics
```
oc adm top nodes
```

The expected output is

<pre>
jegan@tektutor:~$ <b>oc adm top nodes</b>
<b>NAME                             CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%</b>
master-1.tektutor.tektutor.org   1782m        23%    7618Mi          51%       
master-2.tektutor.tektutor.org   1730m        23%    7356Mi          49%       
master-3.tektutor.tektutor.org   1920m        25%    6831Mi          45%       
worker-1.tektutor.tektutor.org   280m         5%     1221Mi          8%        
worker-2.tektutor.tektutor.org   234m         4%     1210Mi          8%        
</pre>

Actually, the lab setup you are using is much more powerful than my local lab.  As my local lab workstation has 48 Virtual Cores, 128 GB RAM and 1 TB SSD, while the training lab that you are using has got 64 Virtual Cores, 512 GB RAM and 6 TB SSD.  Hence the above output would vary, which is expected.

## 🍿Demo - Removing worker role from master node

:x: Please don't attempt this in our training lab 🔴🔴🔴

However, I'll give a hands-on demo from my local lab environment.

Before removing the worker role from master nodes
<pre>
jegan@tektutor:~$ <b>oc get nodes</b>
<b>NAME                             STATUS   ROLES           AGE   VERSION</b>
master-1.tektutor.tektutor.org   Ready    <b>master,worker</b>   62m   v1.22.3+fdba464
master-2.tektutor.tektutor.org   Ready    <b>master,worker</b>   63m   v1.22.3+fdba464
master-3.tektutor.tektutor.org   Ready    <b>master,worker</b>   63m   v1.22.3+fdba464
worker-1.tektutor.tektutor.org   Ready    worker          44m   v1.22.3+fdba464
worker-2.tektutor.tektutor.org   Ready    worker          45m   v1.22.3+fdba464
</pre>

🍿Demo - Let's remove the worker role from the master nodes

:x: Please don't attempt this in our training lab. This will affect the overall number of Pods that can be deployed in our OpenShift cluster.  🔴🔴🔴

However, I'll give a hands-on demo from my local lab environment.

```
oc patch schedulers.config.openshift.io/cluster --type merge -p '{"spec":{"mastersSchedulable":false}}'
```

After removing the worker role from master nodes

<pre>
jegan@tektutor:~$ <b>oc patch schedulers.config.openshift.io/cluster --type merge -p '{"spec":{"mastersSchedulable":false}}'</b>
scheduler.config.openshift.io/cluster patched
jegan@tektutor:~$ <b>oc get nodes</b>
<b>NAME                             STATUS   ROLES    AGE   VERSION</b>
master-1.tektutor.tektutor.org   Ready    <b>master</b>   86m   v1.22.3+fdba464
master-2.tektutor.tektutor.org   Ready    <b>master</b>   88m   v1.22.3+fdba464
master-3.tektutor.tektutor.org   Ready    <b>master</b>   87m   v1.22.3+fdba464
worker-1.tektutor.tektutor.org   Ready    worker   68m   v1.22.3+fdba464
worker-2.tektutor.tektutor.org   Ready    worker   69m   v1.22.3+fdba464
</pre>

##🍿Demo - Adding worker role to the master nodes

:x: Please don't attempt this in our training lab. This will affect the overall number of Pods that can be deployed in our OpenShift cluster 🔴🔴🔴

However, I'll give a hands-on demo from my local lab environment.

Before adding the worker role to the master nodes

<pre>
jegan@tektutor:~$ <b>oc get nodes</b>
<b>NAME                             STATUS   ROLES    AGE   VERSION</b>
master-1.tektutor.tektutor.org   Ready    <b>master</b>   86m   v1.22.3+fdba464
master-2.tektutor.tektutor.org   Ready    <b>master</b>   88m   v1.22.3+fdba464
master-3.tektutor.tektutor.org   Ready    <b>master</b>   87m   v1.22.3+fdba464
worker-1.tektutor.tektutor.org   Ready    worker   68m   v1.22.3+fdba464
worker-2.tektutor.tektutor.org   Ready    worker   69m   v1.22.3+fdba464
</pre>

Now let's add the worker role to all the master nodes in the OpenShift cluster

:x: Please don't attempt this in our training lab 🔴🔴🔴

However, I'll give a hands-on demo from my local lab environment.

```
oc patch schedulers.config.openshift.io/cluster --type merge -p '{"spec":{"mastersSchedulable":true}}'
```

After adding the worker role to the master nodes

<pre>
jegan@tektutor:~$ <b>oc patch schedulers.config.openshift.io/cluster --type merge -p '{"spec":{"mastersSchedulable":true}}'</b>
scheduler.config.openshift.io/cluster patched
jegan@tektutor:~$ <b>oc get nodes</b>
<b>NAME                             STATUS   ROLES           AGE   VERSION</b>
master-1.tektutor.tektutor.org   Ready    <b>master,worker</b>   91m   v1.22.3+fdba464
master-2.tektutor.tektutor.org   Ready    <b>master,worker</b>   92m   v1.22.3+fdba464
master-3.tektutor.tektutor.org   Ready    <b>master,worker</b>   91m   v1.22.3+fdba464
worker-1.tektutor.tektutor.org   Ready    worker          73m   v1.22.3+fdba464
worker-2.tektutor.tektutor.org   Ready    worker          74m   v1.22.3+fdba464
</pre>

##🍿Alternatively, you may also edit this to remove the worker role from Master nodes

:x: Please don't attempt this in our training lab 🔴🔴🔴

However, I'll give a hands-on demo from my local lab environment.

Currently, in my cluster master nodes have worker role.

<pre>
jegan@tektutor:~$ <b>oc get nodes</b>
<b>NAME                             STATUS   ROLES           AGE   VERSION</b>
master-1.tektutor.tektutor.org   Ready    <b>master,worker</b>   91m   v1.22.3+fdba464
master-2.tektutor.tektutor.org   Ready    <b>master,worker</b>   92m   v1.22.3+fdba464
master-3.tektutor.tektutor.org   Ready    <b>master,worker</b>   91m   v1.22.3+fdba464
worker-1.tektutor.tektutor.org   Ready    worker          73m   v1.22.3+fdba464
worker-2.tektutor.tektutor.org   Ready    worker          74m   v1.22.3+fdba464
</pre>

:x: Please don't attempt this in our training lab 🔴🔴🔴

However, I'll give a hands-on demo from my local lab environment.

We can remove the worker role from master as shown below

```
oc edit schedulers.config.openshift.io cluster
```

The expected output is
<pre>
  1 # Please edit the object below. Lines beginning with a '#' will be ignored,
  2 # and an empty file will abort the edit. If an error occurs while saving this file will be
  3 # reopened with the relevant failures.
  4 #
  5 apiVersion: config.openshift.io/v1
  6 kind: Scheduler
  7 metadata:
  8   creationTimestamp: "2022-02-18T11:57:59Z"
  9   generation: 4
 10   name: cluster
 11   resourceVersion: "70128"
 12   uid: c5810f75-bc59-45f2-84bb-7c1d5b1b4bcf
 13 spec:
 14   <b>mastersSchedulable: true</b>
 15   policy:
 16     name: ""
 17 status: {}
</pre>

In order to remove the worker role from Master nodes, the masterSchedulable flag must be updated to false and save the live configuration in the cluster.

After editing, the live configuration will look as shown below

The expected output is

<pre>
  1 # Please edit the object below. Lines beginning with a '#' will be ignored,
  2 # and an empty file will abort the edit. If an error occurs while saving this file will be
  3 # reopened with the relevant failures.
  4 #
  5 apiVersion: config.openshift.io/v1
  6 kind: Scheduler
  7 metadata::heavy_dollar_sign:
  8   creationTimestamp: "2022-02-18T11:57:59Z"
  9   generation: 4
 10   name: cluster
 11   resourceVersion: "70128"
 12   uid: c5810f75-bc59-45f2-84bb-7c1d5b1b4bcf
 13 spec:
 14   <b>mastersSchedulable: false</b>
 15   policy:
 16     name: ""
 17 status: {}
</pre>

If you list the nodes after removing the worker role from master nodes, the output expected is shown below

<pre>
jegan@tektutor:~$ <b>oc edit schedulers.config.openshift.io cluster</b>
scheduler.config.openshift.io/cluster edited
jegan@tektutor:~$ <b>oc get nodes</b>
<b>NAME                             STATUS   ROLES    AGE   VERSION</b>
master-1.tektutor.tektutor.org   Ready    <b>master</b>   11h   v1.22.3+fdba464
master-2.tektutor.tektutor.org   Ready    <b>master</b>   11h   v1.22.3+fdba464
master-3.tektutor.tektutor.org   Ready    <b>master</b>   11h   v1.22.3+fdba464
worker-1.tektutor.tektutor.org   Ready    worker   11h   v1.22.3+fdba464
worker-2.tektutor.tektutor.org   Ready    worker   11h   v1.22.3+fdba464
</pre>

## ⛹️‍ Lab - Listing the existing projects in OpenShift cluster
```
oc get projects
```

The expected output is

<pre>
jegan@tektutor:~$ <b>oc get projects</b>
<b>NAME                                               DISPLAY NAME   STATUS</b>
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

## ⛹️‍♂️ Lab - Creating a project from command line

Though using your name as project name is neither professional nor a best practice. For this training, I
would suggest use your name as 10 participants are sharing a single OpenShift cluster.  Using your name
as project name, helps other participants using the same cluster to identify the projects they created
vs other participants.

This also helps unintented deletion of projects created by other participants.

```
oc new-project jegan --description="Projects created by Jegan" --display-name="Jegan's Project"
```
In the above command description and display name are optional.

The expected output is
<pre>
jegan@tektutor:~$ <b>oc new-project jegan</b>
Already on project "jegan" on server "https://api.tektutor.tektutor.org:6443".

You can add applications to this project with the 'new-app' command. For example, try:

    oc new-app rails-postgresql-example

to build a new example application in Ruby. Or use kubectl to deploy a simple Kubernetes application:

    kubectl create deployment hello-node --image=k8s.gcr.io/serve_hostname
</pre>


## ⛹️‍ Lab - Creating an application from an container image
```
oc new-app twalter/openshift-nginx:stable --name nginx
```
In the above "twalter/openshift-nginx:stable" is a Docker Image and "nginx" is the name of the deployment.

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
jegan@tektutor:~$ <b>oc status</b>
In project jegan on server https://api.tektutor.tektutor.org:6443

svc/nginx - 172.30.155.175 ports 80, 8081
  deployment/nginx deploys istag/nginx:stable 
    deployment #2 running for 47 seconds - 1 pod
    deployment #1 deployed 52 seconds ago


1 info identified, use 'oc status --suggest' to see details.
</pre>

## ⛹️‍♀️ Lab - List the deployments under your project

```
oc get deploy
```

The expected output is
<pre>
jegan@tektutor:~$<b> oc get deploy</b>
<b>NAME    READY   UP-TO-DATE   AVAILABLE   AGE</b>
nginx   1/1     1            1           97s
</pre>

## ⛹️‍♂️ Lab - List the replicasets under your project

```
oc get rs
```

The expected output is
<pre>
jegan@tektutor:~$ <b>oc get rs</b>
<b>NAME               DESIRED   CURRENT   READY   AGE</b>
nginx-5dd56f5c87   1         1         1       96s
nginx-6f99d9668b   0         0         0       101s
</pre>


## ⛹️‍♀️ Lab - List the pods in your project

```
oc get po
```

The expected output is

<pre>
jegan@tektutor:~$ <b>oc get po</b>
<b>NAME                     READY   STATUS    RESTARTS   AGE</b>
nginx-5dd56f5c87-qg9vv   1/1     Running   0          99s
</pre>

## ⛹️‍♂️ Lab - Listing deployment, replicaset and pods
```
oc get deploy,rs,po
```

## ⛹️‍♀️ Lab - Find details of a pod 

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

## ⛹️‍♂️ Lab - Find details of a replicaset
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

## ⛹️‍♂️ Lab - Finding details of a deployment
```
oc describe deploy/nginx
```

The expected output is

<pre>jegan@tektutor:~$ <b>oc get deploy</b>
<b>NAME    READY   UP-TO-DATE   AVAILABLE   AGE</b>
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

## ⛹️‍♀️ Lab - Scaling up a deployment
```
oc scale deploy nginx --replicas=5
```

The expected output is
<pre>
jegan@tektutor:~$ <b>oc get deploy</b>
<b>NAME    READY   UP-TO-DATE   AVAILABLE   AGE</b>
nginx   1/1     1            1           14m
jegan@tektutor:~$ <b>oc scale deploy nginx --replicas=5</b>
deployment.apps/nginx scaled
jegan@tektutor:~$ <b>oc get po</b>
<b>NAME                     READY   STATUS              RESTARTS   AGE</b>
nginx-5dd56f5c87-4jq5q   0/1     ContainerCreating   0          3s
nginx-5dd56f5c87-qg9vv   1/1     Running             0          14m
nginx-5dd56f5c87-sg57k   1/1     Running             0          3s
nginx-5dd56f5c87-sv8bj   0/1     ContainerCreating   0          3s
nginx-5dd56f5c87-zb5cw   1/1     Running             0          3s
jegan@tektutor:~$ <b>oc get po -w</b>
<b>NAME                     READY   STATUS    RESTARTS   AGE</b>
nginx-5dd56f5c87-4jq5q   1/1     Running   0          6s
nginx-5dd56f5c87-qg9vv   1/1     Running   0          14m
nginx-5dd56f5c87-sg57k   1/1     Running   0          6s
nginx-5dd56f5c87-sv8bj   1/1     Running   0          6s
nginx-5dd56f5c87-zb5cw   1/1     Running   0          6s
</pre>


## ⛹️‍♀️ Lab - Scaling down a deployment
List the deployment
```
oc get deploy
```
The expected output is
<pre>
jegan@tektutor:~/tekton$ <b>oc get deploy</b>
<b>NAME    READY   UP-TO-DATE   AVAILABLE   AGE</b>
nginx   5/5     5            5           4m41s
</pre>

Before scaling down
<pre>
jegan@tektutor:~/tekton$ oc get po -w
NAME                     READY   STATUS    RESTARTS   AGE
nginx-5dd56f5c87-9nkzz   1/1     Running   0          4s
nginx-5dd56f5c87-qswvs   1/1     Running   0          4s
nginx-5dd56f5c87-s4txx   1/1     Running   0          4s
nginx-5dd56f5c87-vg7br   1/1     Running   0          56s
nginx-5dd56f5c87-wp95s   1/1     Running   0          4s
</pre>

```
oc scale deploy nginx --replicas=2
```

After Scaling down, the expected output is
<pre>
jegan@tektutor:~/tekton$ <b>oc scale deploy nginx --replicas=2</b>
deployment.apps/nginx scaled
jegan@tektutor:~/tekton$ <b>oc get po</b>
<b>NAME                     READY   STATUS    RESTARTS   AGE</b>
nginx-5dd56f5c87-vtd8x   1/1     Running   0          117s
nginx-5dd56f5c87-xnc96   1/1     Running   0          117s
</pre>
