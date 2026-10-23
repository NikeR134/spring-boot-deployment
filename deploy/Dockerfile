FROM eclipse-temurin:21-jre

WORKDIR /app
COPY target/spring-boot-conditional-profile-*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "/app/app.jar"]

