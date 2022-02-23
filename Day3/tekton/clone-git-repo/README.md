## Executing the git clone taskrun
```
cd ~/openshift-tekton-feb-2022
git pull
cd Day3/tekton/clone-git-repo

oc create -f git-clone-taskrun.yml --save-config=true
```

The expected outupt is

<pre>
jegan@tektutor:~/tekton/Day3/tekton/clone-git-repo$ <b>oc create -f git-clone-taskrun.yml --save-config=true</b>
taskrun.tekton.dev/git-clone-9txdd created
</pre>
