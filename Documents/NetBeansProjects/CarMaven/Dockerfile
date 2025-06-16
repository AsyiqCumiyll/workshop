# Step 1: Build WAR using Maven
FROM maven:3.9.6-eclipse-temurin-11 AS build

WORKDIR /app

# Copy Maven project files
COPY pom.xml .
COPY src ./src

# Build the project (skip tests to speed up)
RUN mvn clean package -DskipTests

# Step 2: Deploy WAR to Tomcat
FROM tomcat:9.0-jdk17

# Clean default apps
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy WAR as ROOT.war
COPY --from=build /app/target/CarMaven.war /usr/local/tomcat/webapps/ROOT.war

# Railway will expose this port
EXPOSE 8080

CMD ["catalina.sh", "run"]

