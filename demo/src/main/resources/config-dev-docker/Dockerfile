FROM bellsoft/liberica-openjdk-alpine:21.0.3

WORKDIR /app

COPY demo.jar /app/demo.jar

EXPOSE 8081

ENTRYPOINT ["java", "-jar", "demo.jar"]