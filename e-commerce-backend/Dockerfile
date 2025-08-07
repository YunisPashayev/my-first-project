FROM gradle:7.6.1-jdk17 AS build

WORKDIR /app

COPY e-commerce-backend/build.gradle e-commerce-backend/settings.gradle e-commerce-backend/gradle.properties ./
COPY e-commerce-backend/gradle ./gradle

RUN gradle --no-daemon dependencies

COPY e-commerce-backend/src ./src

RUN gradle --no-daemon bootJar

FROM eclipse-temurin:17-jre-focal

WORKDIR /app

COPY --from=build /app/build/libs/*.jar app.jar

ENTRYPOINT ["java", "-jar", "app.jar"]