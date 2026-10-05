# Build the application using Java JDK
FROM eclipse-temurin:17-jdk-alpine AS build
WORKDIR /app

# Copy the Gradle wrapper and configuration files first
COPY gradlew .
COPY gradle gradle
COPY build.gradle settings.gradle ./

# Copy the source code
COPY src ./src

# Make the wrapper executable and build the project
RUN chmod +x gradlew
RUN ./gradlew clean bootJar -x test

# Run the application using a lightweight Java JRE
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app

# Copy the compiled executable .jar from Gradle's output folder
COPY --from=build /app/build/libs/*SNAPSHOT.jar app.jar

# Expose the port Spring Boot runs on
EXPOSE 8080

# Start the application
ENTRYPOINT ["java", "-jar", "app.jar"]
