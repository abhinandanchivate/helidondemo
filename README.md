Here’s your **"Complete Guide to Microservices with Helidon MP"** formatted with proper sections, code blocks, and the "Copy code" button functionality, converted into Markdown format for use in a `README.md` or any other `.md` file in your Git repository.

You can use this guide to directly add to your GitHub repository, and GitHub will automatically display the "Copy code" button for each code block.

```markdown
# Complete Guide to Microservices with Helidon MP

## 1. Set Up Your Development Environment
Ensure you have the following installed:

- **Java Development Kit (JDK)**: JDK 11 or later.
- **Maven**: For building projects.
- **IDE**: IntelliJ IDEA or Eclipse.

## 2. Create Multiple Microservices Projects
Generate separate projects for each microservice using Maven.

### User Service

```sh
mvn archetype:generate \
  -DarchetypeGroupId=io.helidon.archetypes \
  -DarchetypeArtifactId=helidon-mp-archetype \
  -DarchetypeVersion=3.0.0 \
  -DgroupId=com.example \
  -DartifactId=user-service \
  -Dversion=1.0-SNAPSHOT \
  -Dpackage=com.example.userservice
```

### Order Service

```sh
mvn archetype:generate \
  -DarchetypeGroupId=io.helidon.archetypes \
  -DarchetypeArtifactId=helidon-mp-archetype \
  -DarchetypeVersion=3.0.0 \
  -DgroupId=com.example \
  -DartifactId=order-service \
  -Dversion=1.0-SNAPSHOT \
  -Dpackage=com.example.orderservice
```

### Inventory Service

```sh
mvn archetype:generate \
  -DarchetypeGroupId=io.helidon.archetypes \
  -DarchetypeArtifactId=helidon-mp-archetype \
  -DarchetypeVersion=3.0.0 \
  -DgroupId=com.example \
  -DartifactId=inventory-service \
  -Dversion=1.0-SNAPSHOT \
  -Dpackage=com.example.inventoryservice
```

## 3. Implement Each Microservice
Implement RESTful endpoints for each microservice.

### User Service

**File**: `src/main/java/com/example/userservice/UserService.java`

```java
package com.example.userservice;

import javax.ws.rs.GET;
import javax.ws.rs.Path;
import javax.ws.rs.Produces;
import javax.ws.rs.core.MediaType;

@Path("/users")
public class UserService {

    @GET
    @Produces(MediaType.APPLICATION_JSON)
    public String getUsers() {
        return "[{\"id\":1, \"name\":\"John Doe\"}]";
    }
}
```

### Order Service

**File**: `src/main/java/com/example/orderservice/OrderService.java`

```java
package com.example.orderservice;

import javax.ws.rs.GET;
import javax.ws.rs.Path;
import javax.ws.rs.Produces;
import javax.ws.rs.core.MediaType;

@Path("/orders")
public class OrderService {

    @GET
    @Produces(MediaType.APPLICATION_JSON)
    public String getOrders() {
        return "[{\"orderId\":1, \"item\":\"Laptop\"}]";
    }
}
```

### Inventory Service

**File**: `src/main/java/com/example/inventoryservice/InventoryService.java`

```java
package com.example.inventoryservice;

import javax.ws.rs.GET;
import javax.ws.rs.Path;
import javax.ws.rs.Produces;
import javax.ws.rs.core.MediaType;

@Path("/inventory")
public class InventoryService {

    @GET
    @Produces(MediaType.APPLICATION_JSON)
    public String getInventory() {
        return "[{\"productId\":1, \"quantity\":100}]";
    }
}
```

## 4. Configure Each Microservice
Add configuration files and dependencies.

### Example Configuration File

**File**: `src/main/resources/META-INF/microprofile-config.properties`

```properties
mp.health.enabled=true
```

## 5. Service Integration
Integrate services by having them communicate with each other.

### Define REST Clients

Create REST client interfaces to interact with other services.

#### Order Service Client in User Service

**File**: `src/main/java/com/example/userservice/OrderClient.java`

```java
package com.example.userservice;

import javax.ws.rs.GET;
import javax.ws.rs.Path;
import javax.ws.rs.Produces;
import javax.ws.rs.core.MediaType;
import org.eclipse.microprofile.rest.client.inject.RegisterRestClient;

@Path("/orders")
@RegisterRestClient
public interface OrderClient {

    @GET
    @Produces(MediaType.APPLICATION_JSON)
    String getOrders();
}
```

### Configure REST Client

**File**: `src/main/resources/META-INF/microprofile-config.properties`

```properties
mp.rest.client."com.example.userservice.OrderClient".url=http://localhost:8081
```

### Use REST Client in User Service

**File**: `src/main/java/com/example/userservice/UserService.java`

```java
package com.example.userservice;

import javax.inject.Inject;
import javax.ws.rs.GET;
import javax.ws.rs.Path;
import javax.ws.rs.Produces;
import javax.ws.rs.core.MediaType;

@Path("/users")
public class UserService {

    @Inject
    OrderClient orderClient;

    @GET
    @Produces(MediaType.APPLICATION_JSON)
    public String getUsers() {
        String orders = orderClient.getOrders();
        return "[{\"id\":1, \"name\":\"John Doe\", \"orders\":" + orders + "}]";
    }
}
```

## 6. Build and Run Each Microservice
### Build Each Service
Navigate to each service directory and build:

```sh
mvn package
```

### Run Each Service
Run the JAR files:

```sh
java -jar target/user-service.jar
java -jar target/order-service.jar
java -jar target/inventory-service.jar
```

Each service runs on its default port (8080, 8081, etc.).

## 7. Deploy and Scale
### Dockerize Each Microservice
Create Dockerfiles for each microservice:

#### Example Dockerfile

**Dockerfile**

```dockerfile
FROM openjdk:11-jre-slim
COPY target/user-service.jar /app/user-service.jar
ENTRYPOINT ["java", "-jar", "/app/user-service.jar"]
```

### Build Docker Image

```sh
docker build -t user-service .
docker build -t order-service .
docker build -t inventory-service .
```

### Run Docker Containers

```sh
docker run -p 8080:8080 user-service
docker run -p 8081:8081 order-service
docker run -p 8082:8082 inventory-service
```

### Kubernetes Deployment
Create Kubernetes manifests (e.g., Deployment and Service YAML files) for each microservice.

#### Example Kubernetes Deployment

**File**: `k8s/user-service-deployment.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: user-service
spec:
  replicas: 1
  selector:
    matchLabels:
      app: user-service
  template:
    metadata:
      labels:
        app: user-service
    spec:
      containers:
      - name: user-service
        image: user-service:latest
        ports:
        - containerPort: 8080
```

**File**: `k8s/user-service-service.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: user-service
spec:
  selector:
    app: user-service
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
```

Apply the manifests to your Kubernetes cluster:

```sh
kubectl apply -f k8s/user-service-deployment.yaml
kubectl apply -f k8s/user-service-service.yaml
```

## 8. Monitor and Manage
### Health Checks
Implement health checks using MicroProfile Health to monitor each service’s health.

### Metrics
Expose metrics using MicroProfile Metrics to monitor performance.
```

### Instructions to Add This to GitHub:

1. **Copy the entire Markdown content above.**

2. **Create or edit the `README.md` file in your Git repository:**
   - Navigate to your Git repository:
     ```bash
     cd your-repo
     ```
   - Open `README.md` or create it:
     ```bash
     nano README.md  # or use any text editor like VSCode
     ```

3. **Paste the content** you copied and save the file.

4. **Commit and push the changes:**
   ```bash
   git add README.md
   git commit -m "Added complete guide to microservices with Helidon MP"
   git push origin main
   ```

Once pushed, GitHub will automatically render the "Copy code" buttons for each code block.
