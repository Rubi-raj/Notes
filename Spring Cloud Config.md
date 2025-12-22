# Spring Cloud Config

## Spring Cloud Config Server

Bellow java code and properties is enough to configure Spring cloud config server.

```java

@SpringBootApplication
@EnableConfigServer
public class ConfigServer {
    public static void main(String[] args) {
        SpringApplication.run(ConfigServer.class, args);
    }
}
```

```propeties
spring.application.name: config-server
server.port: 8888
spring.cloud.config.server.git.uri: file://${user.home}/config-repo
```

### Dependency

```xml

<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>{spring-cloud-version}</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>

<dependencies>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-config</artifactId>
</dependency>
</dependencies>
```

### URL

**Syntax:**
`http://localhost:8888/<file-name>/<profile>` <br>
_eg:-_ `http://localhost:8888/application/default`
