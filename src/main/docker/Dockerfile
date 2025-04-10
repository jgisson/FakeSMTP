FROM eclipse-temurin:21-jre-ubi9-minimal

RUN mkdir -p /output

COPY fakeSMTP-2.1-SNAPSHOT.jar /fakeSMTP.jar

VOLUME /output

EXPOSE 25

ENTRYPOINT ["java","-jar","/fakeSMTP.jar","--background", "--output-dir", "/output", "--port", "25", "--start-server"]
