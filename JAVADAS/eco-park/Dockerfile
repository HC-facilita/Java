FROM maven:3.9.6-eclipse-temurin-21 as builder
 
WORKDIR /app
COPY . .
WORKDIR /app/JAVADAS/eco-park
RUN mvn clean package -DskipTests
 
FROM eclipse-temurin:21-jre
WORKDIR /app
COPY --from=builder /app/JAVADAS/eco-park/target/quarkus-app/lib/ /deployments/lib/
COPY --from=builder /app/JAVADAS/eco-park/target/quarkus-app/*.jar /deployments/
COPY --from=builder /app/JAVADAS/eco-park/target/quarkus-app/app/ /deployments/app/
COPY --from=builder /app/JAVADAS/eco-park/target/quarkus-app/quarkus/ /deployments/quarkus/
 
EXPOSE 8080
CMD ["java", "-jar", "/deployments/quarkus-run.jar"]