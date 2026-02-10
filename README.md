# Spring Boot Web Server

A minimal Spring Boot web server application.

## Versions
- Java: 17.0.18 (Eclipse Adoptium)
- Spring Boot: 2.7.14
- Embedded Tomcat: 9.0.78

## Build and Run

### Using Maven
```bash
mvn clean package
java -jar target/springboot-webserver-1.0.0.jar
```

### Using Docker
```bash
docker build -t springboot-webserver .
docker run -p 8080:8080 springboot-webserver
```


# Use nsenter to enter container namespace (when curl not available in container)
# Get container PID
```bash
docker inspect -f '{{.State.Pid}}' <container_id>
# Enter network namespace and run curl from host
sudo nsenter -t <pid> -n curl http://localhost:3000

OR 
sudo nsenter -t $(docker inspect -f '{{.State.Pid}}' f046b842c97f) -n curl http://localhost:8080
```


### Using Docker Compose
```bash
docker-compose up --build
```

## Endpoints
- `http://localhost:8080/` - Home endpoint with hostname and IP
- `http://localhost:8080/health` - Health check endpoint
- `http://localhost:8080/actuator/health` - Spring Actuator health endpoint

## Configuration
The server binds to `0.0.0.0:8080` by default. You can modify this in `src/main/resources/application.properties`.
