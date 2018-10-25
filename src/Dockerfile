FROM tomcat:8.5

MAINTAINER finde

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils

# Liferay 7 requires a full JDK 8 installation
RUN apt-get -qq update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    openjdk-8-jdk

#RUN ln -s /usr/local/tomcat /opt/tomcat

COPY tomcat-users.xml /usr/local/tomcat/conf/
COPY context.xml /usr/local/tomcat/webapps/manager/META-INF/
COPY ../../../Downloads/liferay/libs /usr/local/tomcat/lib/ext/

COPY setenv.sh /usr/local/tomcat/bin/
COPY ROOT.xml /usr/local/tomcat/conf/Catalina/localhost/
COPY catalina.properties /usr/local/tomcat/conf/
COPY catalina.policy /usr/local/tomcat/conf/
COPY server.xml /usr/local/tomcat/conf/

COPY portal-setup-wizard.properties /usr/local/

WORKDIR "/usr/local/tomcat/bin"
RUN chmod a+x *.sh
WORKDIR "/usr/local/tomcat/"

#COPY liferay.war /usr/local/tomcat/webapps/

COPY ../../../Downloads/liferay/osgi /usr/local/osgi/

#VOLUME ["/usr/local/tomcat/webapps"]

EXPOSE 8080
EXPOSE 8005
EXPOSE 8009
