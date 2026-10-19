FROM maven:3.10-eclipse-temurin-25-noble AS builder

WORKDIR /usr/src/api
COPY pom.xml .
RUN mvn -B dependency:go-offline

COPY . .
RUN mvn package

# app
FROM eclipse-temurin:25-jre

WORKDIR /app
COPY --from=builder /usr/src/api/target/products-api-0.1.0.jar .

EXPOSE 80
ENTRYPOINT ["java", "-jar", "/app/products-api-0.1.0.jar"]

ENV JRE_VERSION="11.0.12" \
    APP_VERSION="0.4.0"