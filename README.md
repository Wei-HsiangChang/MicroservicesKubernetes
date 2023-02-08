# Docker

## Resource: 
https://github.com/in28minutes/spring-microservices-v2/tree/main/05.kubernetes

## Issue
Failed to build docker image locally based on ARM64 architecture

## Issue Solved

Learned from trial and error

Modified the pom file to build docker image locally, and push to DockerHub successfully 

Use Fabric8 Maven Plugin instead of Spring Boot Maven Plugin

#### configuration in pom.xml:
```
<configuration>
   <images>
      <image>
	 <name>${project.name}:${project.version}</name>
	 <build>
	    <from>openjdk:17</from>
	    <assembly>
	       <name>build</name>
	       <descriptorRef>artifact</descriptorRef>
	    </assembly>
	    <ports>
	       <port>8080</port>
	    </ports>
	    <cmd>java -jar build/${project.name}-${project.version}.jar</cmd>
	 </build>
      </image>
   </images>
</configuration>

```
#### Command:
```
- Build the docker image locally:
mvn clean verify -Pbuild-with-fabric-8

- Attach a tag to the image:
docker tag currency-exchange-service-kubernetes:0.0.11-SNAPSHOT michaelspeedrun/currency-exchange-service-kubernetes

- Push docker image to DockerHub
docker push {DockerHub username}/currency-exchange-service-kubernetes
```

## Reference
https://dmp.fabric8.io/