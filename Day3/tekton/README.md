# Day 3 - Tekton

## Tekton CI/CD Pipeline
- Tekton is an opensource knative application that helps you create CI/CD 
  pipeline within Kubernetes/OpenShift cluster.
- Tekton supports both Kubernetes and OpenShift

## Installing Tekton within OpenShift Cluster

🔴 Only one person can perform this task in a Cluster as Tekton is installed cluster wide. 🔴

- From the OpenShift web console, switch to Administrator view and select Operators --> Operators Hub 
  and search for "Red Hat OpenShift Pipelines" and install it.
  
- Once Tekton is installed in your OpenShift cluster it gets listed in the Installed Operators section.

## Installing Tekton CLI tool
```
sudo dnf copr enable chmouel/tektoncd-cli
sudo dnf install tektoncd-cli
```
Once tkn is installed, you may check the version of tkn cli tool by issuing the below command
```
tkn version
```

The expected output is
<pre>
jegan@tektutor:~/tekton/tekton/lab1$ <b>tkn version</b>
Client version: 0.17.2
Pipeline version: v0.28.3
Triggers version: v0.16.1
</pre>


## Tekton Jargons
Custom Resources added by Tekton project to your OpenShift Cluster

- Step
   - Steps dictates the container that will run as part of the task
   - This is where the actual operations are performed
   - Steps can't be executed independently
   - Steps are always enclosed within a Task
   
- Task
   - Task can be executed independently outside a Pipeline
   - each Task can have one or more Steps
   - Task can be scoped to a Project Scope or Cluster wide
   - Steps are the only required objects to create a Task
   - Tasks can be resused across Pipelines
   - Example:-
       - A Task can clone source code from a GitHub
       - A Task can build an container image, etc.,

- Pipeline
   - collection of Tasks
   - results in an output based on your inputs given to CI/CD pipeline
   - Multiple Tasks in a Pipeline could be executed sequentially one after the other or in parallel
   - Example:-
      - a First Task could clone your source code from your GitHub Repo
      - a Second Task could compile your application
      - a Third Task could run Unit Tests on your compiled application
      - a Fourth Task could package the binaries
      - a Fifth Task could deploy the binaries to a JFrog Artifactory Server or Sonatype Nexus Server

- TaskRun
   - Task can be thought of like a Class, while TaskRun is a running instance of a Task
   - TaskRun helps you supply Task arguments that are required for a Task to run
     
- PipelineRun 
   - Pipeline can be thought of like a Class, while PipelineRun is a running instance of a Pipeline
   - PipelineRun helps you supply Pipeline arguments that are required for a Pipeline while executing a CI/CD Pipeline

## Simple Hello World Task

A simple Hello World Task in Tekton looks as shown below

<pre>
  1 apiVersion: tekton.dev/v1beta1
  2 kind: Task
  3 metadata:
  4   name: echo-hello-world
  5   namespace: jegan
  6 spec:
  7   steps:
  8     - name: echo
  9       image: ubuntu
 10       command:
 11         - echo
 12       args:
 13         - "Hello World"
</pre>

## ⛹️‍♂️ Lab - Creating your first Task using Tekton in OpenShift

Make sure Red Hat OpenShift pipelines Operator is already installed in your Cluster and you have personally installed tkn cli tool on your Linux lab machine before proceeding.

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
