FROM ubuntu:latest

ENV TOMCAT_VERSION 9.0.78
ENV TOMCAT_URL https://archive.apache.org/dist/tomcat/tomcat-9/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz

RUN apt-get update && apt-get install -y wget default-jdk git && apt-get clean

RUN wget -q ${TOMCAT_URL} -O /tmp/tomcat.tar.gz && \
    mkdir /opt/tomcat && \
    tar xzf /tmp/tomcat.tar.gz -C /opt/tomcat --strip-components=1

EXPOSE 8080

WORKDIR /petclinic_btc

RUN git clone https://github.com/youngho1234/petclinic_btc.git .
# COPY ./pom.xml ./

RUN chmod +x ./mvnw
RUN ./mvnw clean package

RUN cp target/*.war /opt/tomcat/webapps
CMD ["/opt/tomcat/bin/catalina.sh", "jpda", "run"]
