FROM jetty:9.4.18-jre11 

ENV    JETTY_HOME=/usr/local/jetty
ENV    JETTY_BASE=/var/lib/jetty

User root

ADD ./api/spapi.war ${JETTY_BASE}/webapps/spapi.war'

#RUN sed -i 's/# jetty.httpConfig.sendServerVersion=true/jetty.httpConfig.sendServerVersion=false/g' /$JETTY_HOME/start.ini
RUN sed -i 's/# jetty.httpConfig.sendServerVersion=true/jetty.httpConfig.sendServerVersion=false/g' /$JETTY_HOME/modules/server.mod
RUN sed -i 's/name="jetty.httpConfig.sendServerVersion" deprecated="jetty.send.server.version" default="true"/name="jetty.httpConfig.sendServerVersion" deprecated="jetty.send.server.version" default="false"/g' /$JETTY_HOME/etc/jetty.xml

RUN apk add --update fontconfig ttf-dejavu

RUN chown jetty:jetty $JETTY_BASE/webapps/spapi.war'
ENV JAVA_OPTIONS="-Xms128m -Xmx1024m -Djetty.resource.dir=$JETTY_BASE/resources"

RUN ln -s /run/secrets/datasource.prod.properties ${JETTY_BASE}/resources/datasource.prod.properties
RUN ln -s /run/secrets/credentials.prod.properties ${JETTY_BASE}/resources/credentials.prod.properties

RUN ln -s /run/secrets/ca.crt ${JETTY_BASE}/resources/ca.crt
RUN ln -s /run/secrets/ca.key ${JETTY_BASE}/resources/ca.key

User jetty
