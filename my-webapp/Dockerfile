FROM maven:3.8.4-openjdk-11-slim AS build
WORKDIR /app
COPY pom.xml .
COPY src/ ./src/
RUN mvn clean package

FROM tomcat:9.0-jdk11-openjdk-slim
COPY --from=build /app/target/my-webapp-1.0-SNAPSHOT.war /usr/local/tomcat/webapps/my-webapp.war 
RUN chmod +x /usr/local/tomcat/bin/catalina.sh

EXPOSE 8080
CMD ["catalina.sh", "run"]
