FROM eclipse-temurin:17-jdk-jammy as build

COPY .mvn .mvn
COPY mvnw .
COPY pom.xml .
COPY src src

RUN apt-get update && apt-get install dos2unix
RUN dos2unix mvnw
RUN ./mvnw -B package

FROM eclipse-temurin:17-jre-jammy

COPY --from=build target/new-api-2.0.0.jar .

EXPOSE 8082

ENTRYPOINT ["java", "-jar", "new-api-2.0.0.jar"]