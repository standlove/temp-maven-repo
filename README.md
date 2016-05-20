# temp-maven-repo
Used for managing dependencies which were managed initially through local-repo (user desktop).

#Installing/Pushing new dependencies
Install required jar properly into this repo through `mvn install`

```sh
mvn install:install-file -DgroupId=[group-id] -DartifactId=[artifact-id] -Dversion=[version] -DmodelVersion=[DmodelVersion] -Dpackaging=[packaging-format] -Dfile=[path-to-file] -DlocalRepositoryPath=[path-to-git-repo]
```

**NOTE : Fill [*] fields**

example: 
```sh
mvn install:install-file -DgroupId=com.topcoder.internal -DartifactId=shared -Dversion=1.0.0 -DmodelVersion=4.0.0 -Dpackaging=jar -Dfile=ap-project-microservice/lib/com/topcoder/internal/shared/1.0.0/shared-1.0.0.jar -DlocalRepositoryPath=temp-maven-repo
```

Commit & Push these changes

#Consuming dependencies from this repo

Remove previous references to local-repo i.e

```xml
  <repository>
          <id>local-repo</id>
          <url>file://${local-lib-repo}</url>
  </repository>
```
Add following 
```xml
  <repository>
      <id>temp-maven-repo</id>
      <url>https://github.com/[username]/[repo-name]/raw/[branch-name]</url>
      <snapshots>
          <enabled>true</enabled>
          <updatePolicy>always</updatePolicy>
      </snapshots>
  </repository>
```
**NOTE : Fill [*] fields**

ex: 
```xml
  <url>https://github.com/phaniram/temp-maven-repo/raw/master</url>
```
Now upon maven should check for required dependencies in above repo and download accordingly.
