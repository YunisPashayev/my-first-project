
FROM gradle:7.6.1-jdk17 AS build


WORKDIR /app


COPY build.gradle settings.gradle gradle.properties ./
COPY gradle ./gradle


RUN gradle --no-daemon dependencies


COPY src ./src


RUN gradle --no-daemon bootJar


FROM eclipse-temurin:17-jre-focal


WORKDIR /app


COPY --from=build /app/build/libs/*.jar app.jar


ENTRYPOINT ["java", "-jar", "app.jar"]