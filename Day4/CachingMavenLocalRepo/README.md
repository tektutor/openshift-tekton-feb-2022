## Create a ConfigMap that captures the login credentials of JFrog Artifactory
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: custom-maven-settings
data:
  settings.xml: |
    <?xml version="1.0" encoding="UTF-8"?>
    <settings>
      <servers>
        <server>
          <id>artifactory</id>
          <username>admin</username>
          <password>Admin@123</password>
        </server>
      </servers>
    </settings>
```

#### Creating Config map from the above file
```
oc create configmap custom-maven-settings --from-file=maven-settings-configmap.yml
oc get cm
```

The expected output is
<pre>
jegan@tektutor:~/tekton/Day4/CachingMavenLocalRepo$ <b>oc create configmap custom-maven-settings --from-file=maven-settings-configmap.yml</b>
configmap/custom-maven-settings created
jegan@tektutor:~/tekton/Day4/CachingMavenLocalRepo$ <b>oc get cm</b>
<b>NAME                       DATA   AGE</b>
custom-maven-settings      1      5s
kube-root-ca.crt           1      5d2h
openshift-service-ca.crt   1      5d2h
</pre>
