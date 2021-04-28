FROM alpine:3.8
MAINTAINER Fernando Queiroz Fonseca <fernando.fonseca@sankhya.com.br>

# Expose Web Port
EXPOSE 8080

# Set environment
ENV JAVA_HOME /opt/jdk
ENV PATH ${PATH}:${JAVA_HOME}/bin
ENV JAVA_PACKAGE server-jre

ENV TOMCAT_VERSION_MAJOR 8
ENV TOMCAT_VERSION_FULL  8.5.14
ENV CATALINA_HOME /opt/tomcat

# Download and install Java
RUN apk --update add openjdk8-jre &&\
    mkdir -p /opt/jdk &&\
    ln -s /usr/lib/jvm/java-1.8-openjdk/bin /opt/jdk &&\
    apk add --update wget &&\
    wget --quiet --no-cookies --no-check-certificate https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_VERSION_MAJOR}/v${TOMCAT_VERSION_FULL}/bin/apache-tomcat-${TOMCAT_VERSION_FULL}.tar.gz &&\
    wget --quiet --no-cookies --no-check-certificate https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_VERSION_MAJOR}/v${TOMCAT_VERSION_FULL}/bin/apache-tomcat-${TOMCAT_VERSION_FULL}.tar.gz.md5 &&\
    md5sum -c apache-tomcat-${TOMCAT_VERSION_FULL}.tar.gz.md5 &&\
    gunzip -c apache-tomcat-${TOMCAT_VERSION_FULL}.tar.gz | tar -xf - -C /opt &&\
    rm -f apache-tomcat-${TOMCAT_VERSION_FULL}.tar.gz apache-tomcat-${TOMCAT_VERSION_FULL}.tar.gz.md5 &&\
    ln -s /opt/apache-tomcat-${TOMCAT_VERSION_FULL} /opt/tomcat &&\
    rm -rf /opt/tomcat/webapps/examples /opt/tomcat/webapps/docs &&\
    cp /home/fernando/workspace/socialbank/SB_CORP/api_sp/target/spapi#v1.war /opt/tomcat/webapps && \
    rm -rf /var/cache/apk/* && \
    apk del wget

# Launch Tomcat on startup
CMD ${CATALINA_HOME}/bin/catalina.sh run
