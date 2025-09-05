# build stage (maven)
FROM maven:3.9.4-eclipse-temurin-17 AS builder
WORKDIR /build
COPY pom.xml .
# copy only needed files to leverage cache
COPY src ./src
RUN mvn -B -DskipTests package

# runtime
FROM eclipse-temurin:17-jdk-jammy
WORKDIR /app
COPY --from=builder /build/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","/app/app.jar"]

