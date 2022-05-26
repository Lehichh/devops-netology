# devops-netology
**Sarkisyan Aleksey**

**Домашнее задание - 09.02 CI\CD**


**Задание 1**


![Задание 1](/dz9.2/soner.PNG)


**Задание 2**


![Задание 2](/dz9.2/nexus.PNG)

[maven-metadata](/dz9.2/maven-metadata.xml) 


**Задание 3**


```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instan>
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.netology.app</groupId>
  <artifactId>simple-app</artifactId>
  <version>1.0-SNAPSHOT</version>
   <repositories>
    <repository>
      <id>my-repo</id>
      <name>maven-public</name>
      <url>http://localhost:8081/repository/maven-public/</url>
    </repository>
  </repositories>
  <dependencies>
     <dependency>
      <groupId>netology</groupId>
      <artifactId>java</artifactId>
      <version>8_282</version>
      <classifier>distrib</classifier>
      <type>tar.gz</type>
    </dependency>
  </dependencies>
</project>
```


![Задание 3](/dz9.2/Maven.PNG)