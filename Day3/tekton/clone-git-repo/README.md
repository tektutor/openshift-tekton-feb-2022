## ⛹️‍♂️ Lab - Executing the git clone taskrun

Let's write a TaskRun as shown below

<pre>
  1 apiVersion: tekton.dev/v1beta1
  2 kind: TaskRun
  3 metadata:
  4   generateName: git-clone-
  5   labels:
  6      tekton.dev/task: git-clone
  7 spec:
  8   taskRef:
  9     name: git-clone
 10   params:
 11     - name: url
 12       value: https://github.com/tektutor/spring-ms.git
 13     - name: revision
 14       value: master
 15   workspaces:
 16     - name: output
 17       emptyDir: {}
</pre>

This taskrun depends on git-clone task from Tekton catalog. Check if you already have the git-clone task installed in your cluster
```
tkn task ls
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/clone-git-repo$ <b>tkn task ls</b>
NAME                          DESCRIPTION              AGE
echo-hello-world                                       10 hours ago
echo-hello-world-multisteps                            2 hours ago
<b>git-clone                     These Tasks are Git...   12 minutes ago</b>
hello-world-with-params                                1 hour ago
source-lister                                          22 minutes ago
</pre>

In case the git-clone is not installed in your cluster, you can install as shown below
```
tkn hub install task git-clone
```

The expected output is

<pre>
jegan@tektutor:~/tekton/Day3/tekton/clone-git-repo$ tkn hub install task git-clone
Task git-clone(0.5) installed in jegan namespace
</pre>

```
cd ~/openshift-tekton-feb-2022
git pull
cd Day3/tekton/clone-git-repo

oc create -f git-clone-taskrun.yml --save-config=true
```
The oc create command will create the taskrun and execute it.

The expected output is

<pre>
jegan@tektutor:~/tekton/Day3/tekton/clone-git-repo$ <b>oc create -f git-clone-taskrun.yml --save-config=true</b>
taskrun.tekton.dev/git-clone-9txdd created
</pre>

Now you may check the output of the task run as shown

```
tkn taskrun ls
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/clone-git-repo$ <b>tkn taskrun ls</b>
NAME                                    STARTED          DURATION     STATUS
<b>git-clone-9txdd                         44 seconds ago   12 seconds   Succeeded</b>
source-lister-run-zlth4                 20 minutes ago   5 seconds    Failed(TaskRunResolutionFailed)
hello-world-with-params-run-s4p9c       1 hour ago       11 seconds   Succeeded
hello-world-with-params-run-stk8k       1 hour ago       11 seconds   Succeeded
echo-hello-world-multisteps-run-9kzvp   2 hours ago      33 seconds   Succeeded
echo-hello-world-run-qzstf              2 hours ago      11 seconds   Succeeded
echoer-run-lgbnt                        10 hours ago     45 seconds   Succeeded
echo-hello-world-task-run               10 hours ago     37 seconds   Succeeded
</pre>

You can check the log either from the webconsole or in cli as shown below

<pre>
jegan@tektutor:~/tekton/Day3/tekton/clone-git-repo$ tkn taskrun logs  git-clone-9txdd
[clone] + '[' false '=' true ]
[clone] + '[' false '=' true ]
[clone] + '[' false '=' true ]
[clone] + CHECKOUT_DIR=/workspace/output/
[clone] + '[' true '=' true ]
[clone] + cleandir
[clone] + '[' -d /workspace/output/ ]
[clone] + rm -rf '/workspace/output//*'
[clone] + rm -rf '/workspace/output//.[!.]*'
[clone] + rm -rf '/workspace/output//..?*'
[clone] + test -z 
[clone] + test -z 
[clone] + test -z 
[clone] + /ko-app/git-init '-url=https://github.com/tektutor/spring-ms.git' '-revision=master' '-refspec=' '-path=/workspace/output/' '-sslVerify=true' '-submodules=true' '-depth=1' '-sparseCheckoutDirectories='
[clone] {"level":"info","ts":1645608813.0448492,"caller":"git/git.go:169","msg":"Successfully cloned https://github.com/tektutor/spring-ms.git @ 9d00d37f0027ecba28c943b5d31dca8b0c5674a1 (grafted, HEAD, origin/master) in path /workspace/output/"}
[clone] {"level":"info","ts":1645608813.095898,"caller":"git/git.go:207","msg":"Successfully initialized and updated submodules in path /workspace/output/"}
[clone] + cd /workspace/output/
[clone] + git rev-parse HEAD
[clone] + RESULT_SHA=9d00d37f0027ecba28c943b5d31dca8b0c5674a1
[clone] + EXIT_CODE=0
[clone] + '[' 0 '!=' 0 ]
[clone] + printf '%s' 9d00d37f0027ecba28c943b5d31dca8b0c5674a1
[clone] + printf '%s' https://github.com/tektutor/spring-ms.git
</pre>

## ⛹️‍♀️ Lab - In this lab we will create a Persistent Volume and Claim

Let's create a PersistentVolume as shown below

🔴 Each one of you need to prefix your name in front of the PersistentVolume. Consider reducing the size to 50Mi. 🔴

```
cd ~/openshift-tekton-feb-2022
git pull
cd Day3/tekton/clone-git-repo

oc apply -f maven-tekton-pv.yml
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/clone-git-repo$ <b>oc apply -f maven-tekton-pv.yml</b>
persistentvolume/maven-tekton-pv created
</pre>

Let's now create the PersistentVolumeClaim as shown below

🔴 Each one of you need to prefix your name in front of the PersistentVolumeClaim. Consider reducing the size to 50Mi. 🔴

```
oc apply -f maven-tekton-pvc.yml
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/clone-git-repo$ <b>oc apply -f maven-tekton-pvc.yml</b>
persistentvolumeclaim/maven-tekton-pvc created
</pre>


Let's list and see the Persistent volume
```
oc get pv
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/clone-git-repo$ <b>oc get pv</b>
<b>NAME              CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                    STORAGECLASS    REASON   AGE</b>
maven-tekton-pv   500Mi      RWX            Retain           Bound    jegan/maven-tekton-pvc   local-storage            9m56s
</pre>

Let's list and see if the Persistent Volume Claim is created
```
oc get pvc
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day3/tekton/clone-git-repo$ <b>oc get pvc</b>
<b>NAME               STATUS   VOLUME            CAPACITY   ACCESS MODES   STORAGECLASS    AGE</b>
maven-tekton-pvc   Bound    maven-tekton-pv   500Mi      RWX            local-storage   9m1s
</pre>
