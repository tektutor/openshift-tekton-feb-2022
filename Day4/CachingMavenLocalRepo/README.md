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
