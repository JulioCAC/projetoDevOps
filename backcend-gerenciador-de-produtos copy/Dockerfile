# Stage 1: Build the application
FROM maven:3.9.7-eclipse-temurin-17 AS builder

# Set the working directory in the container
WORKDIR /app

# Copy the Maven wrapper files
COPY .mvn/ .mvn/

# Copy the Maven project file
COPY pom.xml .

# Copy the source code
COPY src src/

# Build the project and create the JAR file
# Skipping tests to speed up the build process in the Dockerfile
# The application.properties will be bundled inside the JAR
RUN mvn clean package -DskipTests

# Stage 2: Create the runtime image
FROM openjdk:17-jdk-slim

# Set the working directory in the container
WORKDIR /app

# Copy the JAR file from the builder stage
# The JAR name is derived from the pom.xml's artifactId and version
COPY --from=builder /app/target/api-0.0.1-SNAPSHOT.jar app.jar

# Expose the port the application runs on (default for Spring Boot is 8080)
EXPOSE 8080

# Command to run the application
ENTRYPOINT ["java", "-jar", "app.jar"]