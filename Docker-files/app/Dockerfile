FROM tomcat:10-jdk21

LABEL Project="Vprofile"
LABEL Author="Javed"

WORKDIR /usr/local/tomcat

RUN rm -rf webapps/*

COPY target/vprofile-v2.war webapps/ROOT.war

EXPOSE 8080

CMD ["catalina.sh", "run"]

