# Use the official Maven image to build the application
FROM docker.arvancloud.ir/maven:3.8.3-openjdk-17 AS build

# Set the working directory
WORKDIR /app

# Copy the pom.xml and the source code
COPY pom.xml .
COPY src ./src

# Package the application
RUN mvn clean package -DskipTests

# Use a lightweight JRE image to run the application
FROM docker.arvancloud.ir/openjdk:17-jdk-slim

# Set the working directory
WORKDIR /app

# Copy the packaged jar file from the build stage
COPY --from=build /app/target/positionsimulator-0.0.1-SNAPSHOT.jar app.jar

# Expose the application port (change if necessary)
EXPOSE 8080

# Command to run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
