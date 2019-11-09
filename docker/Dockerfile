FROM openjdk:8-jdk-alpine
VOLUME /tmp
ADD rocket-demo-0.0.1-SNAPSHOT.jar app.jar
# -Djava.security.egd=file:/dev/./urandom 可解决tomcat可能启动慢的问题
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
EXPOSE 8081
