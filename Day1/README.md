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

