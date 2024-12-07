FROM maven:3.6.3-jdk-11-slim AS build
WORKDIR /workspace
COPY pom.xml /workspace
COPY src /workspace/src
RUN mvn -B -f pom.xml clean package -DskipTests
FROM openjdk:11-jre-slim
RUN useradd -m -s /bin/bash appuser
USER appuser
COPY --from=build /workspace/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
