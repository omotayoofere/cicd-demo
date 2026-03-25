FROM maven:3.9.9-eclipse-temurin-8 AS builder
WORKDIR /app 
COPY pom.xml .
RUN mvn dependency:go-offline -DskipTests
COPY ./src ./src
RUN mvn install -DskipTests

FROM eclipse-temurin:8-jre
WORKDIR /app 
COPY --from=builder /app/target/book-work-0.0.1-SNAPSHOT.jar ./book-work-0.0.1.jar 
EXPOSE 9000
ENTRYPOINT [ "java", "-jar", "book-work-0.0.1.jar" ]