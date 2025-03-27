# Use the official Maven image to build the application
FROM docker.arvancloud.ir/maven:3.8.3-openjdk-17 AS build

# Set the working directory
WORKDIR /app

# Copy the pom.xml and other necessary files
COPY pom.xml .
COPY src ./src

# Build the application
RUN mvn clean package -DskipTests

# Use a smaller base image for the final image
FROM docker.arvancloud.ir/openjdk:17-jdk-slim

# Set the working directory
WORKDIR /app

# Copy the jar file from the build stage
COPY --from=build /app/target/fleetman-0.0.1-SNAPSHOT.jar ./fleetman.jar

# Expose the application port (change if necessary)
EXPOSE 8080

# Command to run the application
ENTRYPOINT ["java", "-jar", "fleetman.jar"]
