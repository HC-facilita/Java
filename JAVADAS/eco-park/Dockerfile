FROM maven:3.9.6-eclipse-temurin-17 as builder
 
WORKDIR /app

# Copia da estrutura real do GitHub

COPY JAVADAS/eco-park/pom.xml .

COPY JAVADAS/eco-park/src ./src

RUN mvn clean package -DskipTests
 
FROM eclipse-temurin:17-jre

WORKDIR /app

COPY --from=builder /app/target/quarkus-app/lib/ /deployments/lib/

COPY --from=builder /app/target/quarkus-app/*.jar /deployments/

COPY --from=builder /app/target/quarkus-app/app/ /deployments/app/

COPY --from=builder /app/target/quarkus-app/quarkus/ /deployments/quarkus/
 
EXPOSE 8080

CMD ["java", "-jar", "/deployments/quarkus-run.jar"]
 