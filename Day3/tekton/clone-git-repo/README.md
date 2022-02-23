## Executing the git clone taskrun

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
jegan@tektutor:~/tekton/Day3/tekton/clone-git-repo$ tkn task ls
NAME                          DESCRIPTION              AGE
echo-hello-world                                       10 hours ago
echo-hello-world-multisteps                            2 hours ago
<b>git-clone                     These Tasks are Git...   12 minutes ago</b>
hello-world-with-params                                1 hour ago
source-lister                                          22 minutes ago
</pre>
