FROM debian:stretch-slim

# 添加国内源
ADD sources.list /etc/apt/ 

ENV TOMCAT_MAJOR=9 \
    TOMCAT_VERSION=9.0.43\
    TOMCAT_HOME=/opt/tomcat \
    CATALINA_HOME=/opt/tomcat \
    CATALINA_OUT=/dev/null
RUN mkdir -p /usr/share/man/man1

RUN apt-get update && apt-get upgrade -y && apt-get install -y --no-install-recommends \
    curl \
    openjdk-8-jdk \
    openjdk-8-jre && \
    curl -jksSL -o /tmp/apache-tomcat.tar.gz http://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR}/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz && \
    gunzip /tmp/apache-tomcat.tar.gz && \
    tar -C /opt -xf /tmp/apache-tomcat.tar && \
    ln -s /opt/apache-tomcat-${TOMCAT_VERSION} ${TOMCAT_HOME} && \
    rm -rf ${TOMCAT_HOME}/webapps/* && \
    apt-get autoremove --purge -y && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
# ADD F:/java/ROOT /opt/tomcat/webapps/ROOT/
CMD  /opt/tomcat/bin/catalina.sh run
EXPOSE 8080