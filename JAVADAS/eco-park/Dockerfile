# Dockerfile corrigido para estrutura de subpastas

FROM maven:3.9.6-eclipse-temurin-17 as builder
 
WORKDIR /app

COPY Java/JAVADAS/eco-park/pom.xml .

COPY Java/JAVADAS/eco-park/src ./src

RUN mvn clean package -DskipTests
 
FROM registry.access.redhat.com/ubi9/openjdk-21:1.23
 
WORKDIR /app

COPY --from=builder /app/target/quarkus-app/lib/ /deployments/lib/

COPY --from=builder /app/target/quarkus-app/*.jar /deployments/

COPY --from=builder /app/target/quarkus-app/app/ /deployments/app/

COPY --from=builder /app/target/quarkus-app/quarkus/ /deployments/quarkus/
 
EXPOSE 8080

USER 185

ENV JAVA_OPTS_APPEND="-Dquarkus.http.host=0.0.0.0 -Djava.util.logging.manager=org.jboss.logmanager.LogManager"

ENV JAVA_APP_JAR="/deployments/quarkus-run.jar"
 
ENTRYPOINT [ "/opt/jboss/container/java/run/run-java.sh" ]
 