# lab10-
doc file for pom,web,json service

from abhiram ---
PFA, The updated Document which contains the config files and code for the 10th OOPS Program. Few Steps to keep in mind:
1. Proper versions. [Build web module version 4.0] [Tomcat v9 (Download and install) Do not use the old server file.]
2. Download And use Postman to test all the endpoints.
URL example: http://localhost:8080/<Your-Project-name>/home/post
===================================
FROM CHATGPT ---
Steps to Run JAX-RS REST API using Maven in Eclipse
1. Create a Maven Web Project
In Eclipse:
File → New → Maven Project
Check Create a simple project (skip archetype selection) → Next
Fill details:
Group Id: com.api
Artifact Id: RestAPIExample
Packaging: war
Java Version: 11 or 17 (depending on your JDK).
Finish → Eclipse will generate a project with the folder structure.

2. Update pom.xml
Open pom.xml and add dependencies for Jersey + JAX-RS:
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>
    <groupId>com.api</groupId>
    <artifactId>RestAPIExample</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>war</packaging>

    <properties>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <!-- JAX-RS API -->
        <dependency>
            <groupId>jakarta.ws.rs</groupId>
            <artifactId>jakarta.ws.rs-api</artifactId>
            <version>3.1.0</version>
            <scope>provided</scope>
        </dependency>

        <!-- Jersey Implementation -->
        <dependency>
            <groupId>org.glassfish.jersey.containers</groupId>
            <artifactId>jersey-container-servlet</artifactId>
            <version>3.1.2</version>
        </dependency>

        <!-- Optional: JSON support -->
        <dependency>
            <groupId>org.glassfish.jersey.media</groupId>
            <artifactId>jersey-media-json-binding</artifactId>
            <version>3.1.2</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>3.3.2</version>
            </plugin>
        </plugins>
    </build>
</project>
Then → Right-click project → Maven → Update Project (to download dependencies).

3. Add REST Service Class
Inside src/main/java/com/api/JSONService.java:
import jakarta.ws.rs.DELETE;
import jakarta.ws.rs.GET;
import jakarta.ws.rs.POST;
import jakarta.ws.rs.PUT;
import jakarta.ws.rs.Path;
import jakarta.ws.rs.Produces;

@Path("/home")
public class JSONService {

    @GET
    @Produces("text/plain")
    public String getMethod() {
        return "Hello from REST based API";
    }

    @POST
    @Path("/post")
    @Produces("text/plain")
    public String postMethod() {
        return "In the POST method - Hello from REST based API";
    }

    @PUT
    @Path("/put")
    @Produces("text/plain")
    public String putMethod() {
        return "In the PUT method - Hello from REST based API";
    }

    @DELETE
    @Path("/delete")
    @Produces("text/plain")
    public String deleteMethod() {
        return "In the DELETE method - Hello from REST based API";
    }
}
4. Configure web.xml
In src/main/webapp/WEB-INF/web.xml:
<web-app xmlns="http://java.sun.com/xml/ns/javaee"
         version="3.0">
    <servlet>
        <servlet-name>Jersey REST Service</servlet-name>
        <servlet-class>org.glassfish.jersey.servlet.ServletContainer</servlet-class>
        <init-param>
            <param-name>jersey.config.server.provider.packages</param-name>
            <param-value>com.api</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>

    <servlet-mapping>
        <servlet-name>Jersey REST Service</servlet-name>
        <url-pattern>/rest/*</url-pattern>
    </servlet-mapping>
</web-app>



5. Run on Tomcat
Make sure you’ve added Tomcat server in Eclipse (via Window → Preferences → Server → Runtime Environments).
Right-click project → Run As → Run on Server.
Choose Tomcat v9.0 (or v10) → Finish.

6 .Test Endpoints
Open your browser or Postman:
http://localhost:8080/RestAPIExample/rest/home → GET
http://localhost:8080/RestAPIExample/rest/home/post → POST
http://localhost:8080/RestAPIExample/rest/home/put → PUT
http://localhost:8080/RestAPIExample/rest/home/delete → DELETE


