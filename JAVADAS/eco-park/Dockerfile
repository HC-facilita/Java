FROM maven:3.9.6-eclipse-temurin-17 as builder
 
WORKDIR /app
 
RUN find . -name "pom.xml" -exec cp {} . \; && \
    find . -name "src" -type d -exec cp -r {} . \; && \
    mvn clean package -DskipTests
 
FROM eclipse-temurin:17-jre
WORKDIR /app
COPY --from=builder /app/target/quarkus-app/lib/ /deployments/lib/
COPY --from=builder /app/target/quarkus-app/*.jar /deployments/
COPY --from=builder /app/target/quarkus-app/app/ /deployments/app/
COPY --from=builder /app/target/quarkus-app/quarkus/ /deployments/quarkus/
 
EXPOSE 8080
CMD ["java", "-jar", "/deployments/quarkus-run.jar"]