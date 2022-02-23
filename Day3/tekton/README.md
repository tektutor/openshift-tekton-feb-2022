# Day 3 - Tekton

## Tekton CI/CD Pipeline
- Tekton is an opensource knative application that helps you create CI/CD 
  pipeline within Kubernetes/OpenShift cluster.
- Tekton supports both Kubernetes and OpenShift
- is a set of custom kubernetes resources

## Installing Tekton within OpenShift Cluster

🔴 Only one person can perform this task in a Cluster as Tekton is installed cluster wide. 🔴

From the OpenShift web console, switch to Administrator view.  Navigate to Operators --> OperatorHub Menu on the Left side as shown in the screenshot below. In the search text box, you need to type "OpenShift Pipelines" to narrow down the search
![Operators](OCP_Pipeline_Operator.png)

Select "Red Hat OpenShift Pipelines" and Click on Install button.
![Operators](OCP_Pipeline_Install.png)

You may now click on the Install button
![Operators](OCP_Pipeline_Install2.png)
Once you Click on the Install button, you will be taken to below screen

![Operators](OCP_Install3.png)
Once the Installation is complete, it will take you the below page

![Operators](OCP_View_Operator.png)
You may now click on the View Operator button which then takes you to the final page.

![Operators](OCP_View2.png)
![Operators](OCP_View_Operator3.png)

Congratulations! you have installed Tekton in your OpenShift Cluster.


## Installing Tekton CLI tool
```
cd ~/Downloads
wget https://github.com/tektoncd/cli/releases/download/v0.22.0/tkn_0.22.0_Linux_x86_64.tar.gz
tar xvf tkn_0.22.0_Linux_x86_64.tar.gz
mv tkn /usr/local/bin
```
Once tkn is installed, you may check the version of tkn cli tool by issuing the below command
```
tkn version
```

The expected output will be similar to shown below

<pre>
jegan@tektutor:~/tekton/tekton/lab1$ <b>tkn version</b>
Client version: 0.17.2
Pipeline version: v0.28.3
Triggers version: v0.16.1
</pre>

You may see a different version, may be much latest version than my environment.

## Tekton Jargons
Custom Resources added by Tekton project to your OpenShift Cluster

- Step
   - is a Custom Resource added by Tekton to your OpenShift cluster using CRD
   - Steps dictates the container that will run as part of the task
   - This is where the actual operations are performed
   - Steps can't be executed independently
   - Steps are always enclosed within a Task
   - Each Step runs in its own Container
   
- Task
   - is a Custom Resource added by Tekton to your OpenShift cluster using CRD
   - Task can be executed independently outside a Pipeline
   - each Task can have one or more Steps
   - Task can be scoped to a Project Scope or Cluster wide
   - Steps are the only required objects to create a Task
   - Tasks can be resused across Pipelines
   - Each Step in a Task runs in a separate container within the same Pod
   - Example:-
       - A Task can clone source code from a GitHub
       - A Task can build an container image, etc.,

- Pipeline
   - is a Custom Resource added by Tekton to your OpenShift cluster using CRD
   - collection of Tasks
   - results in an output based on your inputs given to CI/CD pipeline
   - Multiple Tasks in a Pipeline could be executed sequentially one after the other or in parallel
   - Example:-
      - a First Task could clone your source code from your GitHub Repo
      - a Second Task could compile your application after the First Task completes successfully
      - a Third Task could run Unit Tests on your compiled application if Second Task succeeds
      - a Fourth Task could package the binaries if Third Task succeeds
      - a Fifth Task could deploy the binaries to a JFrog Artifactory Server or Sonatype Nexus Server if Fourth Task succeeds
      - a Sixth Task could in parallel to Fifth Task can deploy the microservice to staging environment if Fourth Task succeeds

- TaskRun
   - is a Custom Resource added by Tekton to your OpenShift cluster using CRD
   - Task can be thought of like a Class, while TaskRun is a running instance of a Task
   - TaskRun helps you supply Task arguments that are required for a Task to run
     
- PipelineRun 
   - is a Custom Resource added by Tekton to your OpenShift cluster using CRD 
   - Pipeline can be thought of like a Class, while PipelineRun is a running instance of a Pipeline
   - PipelineRun invokes the Pipeline with custom parameter values that Pipeline expects
   - PipelineRun helps you supply Pipeline arguments that are required for a Pipeline while executing a CI/CD Pipeline

## What is a Tekton Trigger?
- Tekton Triggers is a Tekton component that allows you to detect and extract information from events from a variety of sources
- Tekton Triggers can invoke TaskRun and/or PipelineRun with the parameters retrieved from events
- Tekton Triggers is an extension to Tekton Pipelines
- For example:-
    - This helps in triggering a Tekton CI/CD pipeline based on code commit in GitHub repo or similar version control servers

## What is a Tekton Catalog?
 - Reusable Task and Pipeline Resources 

## What is Tekton Dashboard?
 - Web-based Dashboard for Tekton 
 - This needs to installed separately on-need basis
 - As OpenShift already comes with a GUI, this may not be necessary for us.

## Simple Hello World Task

A simple Hello World Task in Tekton looks as shown below

<pre>
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: echo-hello-world
  namespace: jegan
spec:
  steps:
    - name: echo
      image: ubuntu
      command:
        - echo
      args:
        - "Hello World"
</pre>

In the above manifest file, you need to replace "jegan" with your project name.  You need to do this in all the following Lab exercises.

## ⛹️‍♀️ Lab - Clone the tekton Gihub repo
```
cd ~
git clone https://github.com/tektutor/openshift-tekton-feb-2022.git
cd openshift-tekton-feb-2022
ls 
```


## ⛹️‍♂️ Lab - Creating your first Task using Tekton in OpenShift

Make sure "Red Hat OpenShift Pipelines" Operator is already installed in your Cluster and you have to personally install tkn cli tool on your Linux lab machine before proceeding below.

```
cd ~/openshift-tekton-feb-2022
git pull
cd Day3/tekton/hello
oc apply -f hello-world-task.yml
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/hello$ <b>oc apply -f hello-world-task.yml</b>
task.tekton.dev/echo-hello-world created
</pre>

You may now try to list the task using tkn cli utility

```
tkn task list
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/hello$ <b>tkn task list</b>
<b>NAME               DESCRIPTION   AGE</b>
echo-hello-world                 1 minute ago
</pre>

You may also try listing the task using oc cli tool
```
oc get task
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/hello$ <b>oc get task</b>
<b>NAME               AGE</b>
echo-hello-world   92s
</pre>

Executing your first hello-world task

```
tkn task start echo-hello-world
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/hello$ <b>tkn task start echo-hello-world</b>
TaskRun started: <b>echo-hello-world-run-9cwrx</b>

In order to track the TaskRun progress run:
<b>tkn taskrun logs echo-hello-world-run-9cwrx -f -n jegan</b>
</pre>

Let us now check the logs
```
tkn taskrun logs echo-hello-world-run-9cwrx -f -n jegan
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/hello$ <b>tkn taskrun logs echo-hello-world-run-9cwrx -f -n jegan</b>
[echo] <b>Hello World</b>
</pre>

## ⛹️‍♀️ Lab - Running the Task via TaskRun declaratively

TaskRun code looks as shown below,

<pre>
apiVersion: tekton.dev/v1beta1
kind: TaskRun
metadata:
  name: echo-hello-world-task-run
spec:
  taskRef:
    name: echo-hello-world
</pre>

Executing the above TaskRun
```
cd ~/openshift-tekton-feb-2022
git pull
cd Day3/tekton/

oc apply -f hello-taskrun.yml
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/hello-taskrun$ <b>oc apply -f hello-taskrun.yml</b>
taskrun.tekton.dev/echo-hello-world-task-run created
</pre>

Let's now check the status of the TaskRun as shown below
<pre>
jegan@tektutor:~/tekton/Day3/tekton/hello-taskrun$ <b>tkn taskrun list</b>
<b>NAME                        STARTED         DURATION   STATUS</b>
echo-hello-world-task-run   9 seconds ago   ---        Running(Pending)
</pre>

Let's now check detailed status of our TaskRun as shown below

<pre>
jegan@tektutor:~/tekton/Day3/tekton/hello-taskrun$ <b>tkn taskrun describe echo-hello-world-task-run</b>
Name:              echo-hello-world-task-run
Namespace:         jegan
Task Ref:          echo-hello-world
Service Account:   pipeline
Timeout:           1h0m0s
Labels:
 app.kubernetes.io/managed-by=tekton-pipelines
 tekton.dev/task=echo-hello-world

🌡️  Status

STARTED          DURATION     STATUS
59 seconds ago   37 seconds   Succeeded

📨 Input Resources

 No input resources

📡 Output Resources

 No output resources

⚓ Params

 No params

📝 Results

 No results

📂 Workspaces

 No workspaces

🦶 Steps

 NAME     STATUS
 ∙ echo   Completed

🚗 Sidecars

No sidecars
</pre>

If you are curious to the see the output of the task execution, then try this
```
tkn taskrun logs echo-hello-world-task-run
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/hello-taskrun$ <b>tkn taskrun logs echo-hello-world-task-run</b>
[echo] Hello World
</pre>

## ⛹️‍♂️ Lab - Creating a Cluster-wide Task
The cluster task looks as below
<pre>
apiVersion: tekton.dev/v1beta1
kind: ClusterTask 
metadata:
  name: echoer
spec:
  steps:
    - image: alpine
      script: | 
        #!/bin/sh
        echo 'Meeow!! from Tekton 😺🚀'
</pre>

You can directly the create the task from the below folder.
```
cd ~/openshift-tekton-feb-2022
git pull
cd Day3/tekton/cluster-wide-task

oc apply -f cluster-wide-task.yml
```
The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/cluster-wide-task$ <b>oc apply -f cluster-wide-task.yml</b>
clustertask.tekton.dev/echoer created
</pre>

Now let's check if the cluster-wide task that we created is there
```
tkn task list
```
The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/cluster-wide-task$ <b>tkn task list</b>
<b>NAME               DESCRIPTION   AGE</b>
echo-hello-world                 14 minutes ago
</pre>
The reason we don't see the cluster-wide task is, the above command will only show the tasks created within the project namespace
but cluster-wide task is running on the cluster scope. Hence we need to use a different command to see that.

Listing the cluster-wide tasks
```
tkn clustertask ls
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/cluster-wide-task$ tkn clustertask ls
NAME                       DESCRIPTION              AGE
buildah                    Buildah task builds...   48 minutes ago
buildah-1-6-0              Buildah task builds...   48 minutes ago
<b>echoer                                              21 seconds ago</b>
git-cli                    This task can be us...   48 minutes ago
git-clone                  These Tasks are Git...   48 minutes ago
git-clone-1-6-0            These Tasks are Git...   48 minutes ago
helm-upgrade-from-repo     These tasks will in...   48 minutes ago
helm-upgrade-from-source   These tasks will in...   48 minutes ago
jib-maven                  This Task builds Ja...   48 minutes ago
kn                         This Task performs ...   48 minutes ago
kn-1-6-0                   This Task performs ...   48 minutes ago
kn-apply                   This task deploys a...   48 minutes ago
kn-apply-1-6-0             This task deploys a...   48 minutes ago
kubeconfig-creator         This Task do a simi...   48 minutes ago
maven                      This Task can be us...   48 minutes ago
openshift-client           This task runs comm...   48 minutes ago
openshift-client-1-6-0     This task runs comm...   48 minutes ago
pull-request               This Task allows a ...   48 minutes ago
s2i-dotnet                 s2i-dotnet task fet...   48 minutes ago
s2i-dotnet-1-6-0           s2i-dotnet task fet...   48 minutes ago
s2i-go                     s2i-go task clones ...   48 minutes ago
s2i-go-1-6-0               s2i-go task clones ...   48 minutes ago
s2i-java                   s2i-java task clone...   48 minutes ago
s2i-java-1-6-0             s2i-java task clone...   48 minutes ago
s2i-nodejs                 s2i-nodejs task clo...   48 minutes ago
s2i-nodejs-1-6-0           s2i-nodejs task clo...   48 minutes ago
s2i-perl                   s2i-perl task clone...   48 minutes ago
s2i-perl-1-6-0             s2i-perl task clone...   48 minutes ago
s2i-php                    s2i-php task clones...   48 minutes ago
s2i-php-1-6-0              s2i-php task clones...   48 minutes ago
s2i-python                 s2i-python task clo...   48 minutes ago
s2i-python-1-6-0           s2i-python task clo...   48 minutes ago
s2i-ruby                   s2i-ruby task clone...   48 minutes ago
s2i-ruby-1-6-0             s2i-ruby task clone...   48 minutes ago
skopeo-copy                Skopeo is a command...   48 minutes ago
skopeo-copy-1-6-0          Skopeo is a command...   48 minutes ago
tkn                        This task performs ...   48 minutes ago
tkn-1-6-0                  This task performs ...   48 minutes ago
trigger-jenkins-job        The following task ...   48 minutes ago
</pre>

You may also try listing the clustertasks using oc cli tool
```
oc get clustertasks
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/cluster-wide-task$ <b>oc get clustertasks</b>
<b>NAME                       AGE</b>
buildah                    63m
buildah-1-6-0              63m
<b>echoer                     15m</b>
git-cli                    63m
git-clone                  63m
git-clone-1-6-0            63m
helm-upgrade-from-repo     63m
helm-upgrade-from-source   63m
jib-maven                  63m
kn                         63m
kn-1-6-0                   63m
kn-apply                   63m
kn-apply-1-6-0             63m
kubeconfig-creator         63m
maven                      63m
openshift-client           63m
openshift-client-1-6-0     63m
pull-request               63m
s2i-dotnet                 63m
s2i-dotnet-1-6-0           63m
s2i-go                     63m
s2i-go-1-6-0               63m
s2i-java                   63m
s2i-java-1-6-0             63m
s2i-nodejs                 63m
s2i-nodejs-1-6-0           63m
s2i-perl                   63m
s2i-perl-1-6-0             63m
s2i-php                    63m
s2i-php-1-6-0              63m
s2i-python                 63m
s2i-python-1-6-0           63m
s2i-ruby                   63m
s2i-ruby-1-6-0             63m
skopeo-copy                63m
skopeo-copy-1-6-0          63m
tkn                        63m
tkn-1-6-0                  63m
trigger-jenkins-job        63m
</pre>

Let's try describing our clustertask
```
tkn clustertask describe echoer
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/cluster-wide-task$ <b>tkn clustertask describe echoer</b>
Name:   echoer

📨 Input Resources

 No input resources

📡 Output Resources

 No output resources

⚓ Params

 No params

📝 Results

 No results

📂 Workspaces

 No workspaces

🦶 Steps

 ∙ unnamed-0

🗂  Taskruns

 No taskruns
</pre>

Let's now run the task in the current namespace
```
tkn clustertask start echoer --showlog
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/cluster-wide-task$ <b>tkn clustertask start echoer --showlog</b>
TaskRun started: echoer-run-lgbnt
Waiting for logs to be available...

[unnamed-0] Meeow!! from Tekton 😺🚀
</pre>
It might take few seconds to show the above output which is normal as it has to spin a new Pod.

Running the cluster task from other project namespace.
Let's first create a new project as shown below
```
oc new-project jegan-tekton-project
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/cluster-wide-task$ oc new-project jegan-tekton-project
Now using project "jegan-tekton-project" on server "https://api.tektutor.tektutor.org:6443".

You can add applications to this project with the 'new-app' command. For example, try:

    oc new-app rails-postgresql-example

to build a new example application in Ruby. Or use kubectl to deploy a simple Kubernetes application:

    kubectl create deployment hello-node --image=k8s.gcr.io/serve_hostname
</pre>

Now let's run the cluster task in the new project namespaces
```
kubectl config set-context --current --namespace=jegan-tekton-project
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/cluster-wide-task$ <b>kubectl config set-context --current --namespace=jegan-tekton-project</b>
Context "jegan-tekton-project/api-tektutor-tektutor-org:6443/system:admin" modified.
jegan@tektutor:~/tekton/Day3/tekton/cluster-wide-task$ tkn clustertask start echoer --showlog
TaskRun started: echoer-run-7bkbp
Waiting for logs to be available...
<b>[unnamed-0] Meeow!! from Tekton 😺🚀</b>
</pre>

## ⛹️‍♂️ Lab - Printing detailed config view of OpenShift cluster
```
oc config view
```
oc or kubectl can be used interchangingly.  Both tools will give the same results for the above command.

<pre>
jegan@tektutor:~/tekton/Day3/tekton/build-maven-project$ <b>oc config view</b>
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://api.tektutor.tektutor.org:6443
  name: api-tektutor-tektutor-org:6443
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://api.tektutor.tektutor.org:6443
  name: tektutor
contexts:
- context:
    cluster: tektutor
    user: admin
  name: admin
- context:
    cluster: api-tektutor-tektutor-org:6443
    namespace: jegan-tekton-project
    user: system:admin/api-tektutor-tektutor-org:6443
  name: jegan-tekton-project/api-tektutor-tektutor-org:6443/system:admin
- context:
    cluster: api-tektutor-tektutor-org:6443
    namespace: tektontutorial
    user: system:admin/api-tektutor-tektutor-org:6443
  name: jegan/api-tektutor-tektutor-org:6443/system:admin
current-context: jegan-tekton-project/api-tektutor-tektutor-org:6443/system:admin
kind: Config
preferences: {}
users:
- name: admin
  user:
    client-certificate-data: REDACTED
    client-key-data: REDACTED
- name: system:admin/api-tektutor-tektutor-org:6443
  user:
    client-certificate-data: REDACTED
    client-key-data: REDACTED
</pre>

## ⛹️‍♂️ Lab - Printing short and crisp config view of OpenShift cluster
Using oc tool in the place of kubectl also will fetch the same results.
```
kubectl config view --minify
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/build-maven-project$ <b>kubectl config view --minify</b>
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://api.tektutor.tektutor.org:6443
  name: api-tektutor-tektutor-org:6443
contexts:
- context:
    cluster: api-tektutor-tektutor-org:6443
    namespace: jegan-tekton-project
    user: system:admin/api-tektutor-tektutor-org:6443
  name: jegan-tekton-project/api-tektutor-tektutor-org:6443/system:admin
current-context: jegan-tekton-project/api-tektutor-tektutor-org:6443/system:admin
kind: Config
preferences: {}
users:
- name: system:admin/api-tektutor-tektutor-org:6443
  user:
    client-certificate-data: REDACTED
    client-key-data: REDACTED
</pre>

## ⛹️‍♀️ Lab - Extracting namespace i.e project name from the config view
You may also substitute oc in the place of kubectl to observe the same results.
```
kubectl config view --minify | grep namespace
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/build-maven-project$ <b>kubectl config view --minify | grep namespace</b>
    namespace: jegan-tekton-project
</pre>


## ⛹️‍♀️ Lab - Install Maven Task from Tekton Hub
```
tkn hub install task maven
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/build-maven-project$ <b>tkn hub install task maven</b>
Task maven(0.2) installed in jegan-tekton-project namespace
</pre>

## ⛹️‍♂️ Lab - Install git-clone Task from Tekton Hub
```
tkn hub install task git-clone
```
The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/build-maven-project$ <b>tkn hub install task git-clone</b>
Task git-clone(0.5) installed in jegan-tekton-project namespace
</pre>

## ⛹️‍♂️ Lab - Building a maven project and preparing a custom docker image
Let's first verify are we in the correct project
```
kubectl config view --minify | grep namespace
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/build-maven-project$ <b>kubectl config view --minify | grep namespace</b>
    namespace: jegan-tekton-project
</pre>

Let us now create the pipeline in our project namespace
```
jegan@tektutor:~/tekton/Day3/tekton/build-maven-project$ oc apply -f maven-pipeline.yml 
pipeline.tekton.dev/maven-test-pipeline created
pipelinerun.tekton.dev/maven-test-pipeline-run created
```

You may now view the Pipeline as Administrator from the Pipelines section.

