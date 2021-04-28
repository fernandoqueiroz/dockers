FROM alpine:edge

MAINTAINER Fernando Queiroz Fonseca

# Set environment
ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk/
ENV PATH ${PATH}:${JAVA_HOME}/bin

# Download and install Java
RUN apk --update add openjdk11-jre &&\
	apk --update add openjdk11-jdk &&\
    apk add --update jetty-runner

# Launch Tomcat on startup
EXPOSE 8080
CMD ["java","-jar","/usr/local/jetty/start.jar"]
