FROM eclipse-temurin:17-jdk-jammy as build

COPY .mvn .mvn
COPY mvnw .
COPY pom.xml .
COPY src src

RUN apt-get update && apt-get install dos2unix
RUN dos2unix mvnw
RUN ./mvnw -B package

FROM eclipse-temurin:17-jre-jammy

COPY --from=build target/old-api-1.0.0.jar .

EXPOSE 8082

ENTRYPOINT ["java", "-jar", "old-api-1.0.0.jar"]