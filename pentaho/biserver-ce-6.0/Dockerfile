FROM blijblijblij/java:8

MAINTAINER Rogier Wessel, rhwessel@xs4all.nl

ENV MAYOR_VERSION 6.0
ENV MINOR_VERSION 6.0.0.0-353

# Update the APT cache
RUN apt-get update && apt-get upgrade -y

# Set up Pentaho user + directory
RUN useradd -m pentaho
RUN mkdir /opt/pentaho
RUN chown pentaho:pentaho /opt/pentaho

# Install Pentaho Business Analytics
RUN su -c "curl -L http://downloads.sourceforge.net/project/pentaho/Business%20Intelligence%20Server/$MAYOR_VERSION/biserver-ce-$MINOR_VERSION.zip \
  -o /opt/pentaho/biserver-ce.zip && \
  unzip -q /opt/pentaho/biserver-ce.zip \
  -d /opt/pentaho/ && \
  rm -f /opt/pentaho/biserver-ce.zip" pentaho

# Disable first-time startup prompt
RUN rm /opt/pentaho/biserver-ce/promptuser.sh
# Disable daemon mode for Tomcat
RUN sed -i -e 's/\(exec ".*"\) start/\1 run/' /opt/pentaho/biserver-ce/tomcat/bin/startup.sh

# Add libs
ADD mysql-connector-java-5.1.18.jar /opt/pentaho/biserver-ce/tomcat/lib/mysql.jar
ADD postgresql-9.1-901.jdbc4.jar /opt/pentaho/biserver-ce/tomcat/lib/postgresql.jar
ADD vertica-jdk5-6.1.2-0.jar /opt/pentaho/biserver-ce/tomcat/lib/vertica.jar

# Install all the plugins
#RUN wget --no-check-certificate 'https://raw.github.com/pmalves/ctools-installer/master/ctools-installer.sh' -P / -o /dev/null && \
#  chmod +x ctools-installer.sh && \
#  ./ctools-installer.sh -s /opt/pentaho/biserver-ce/pentaho-solutions \
#  -w /opt/pentaho/biserver-ce/tomcat/webapps/pentaho \
#  -c cdf,cda,cde,cgg,sparkl,saiku \
#  -b stable \
#  -y

# Set up runtime options
EXPOSE 8080

ENTRYPOINT ["/opt/pentaho/biserver-ce/start-pentaho.sh"]

USER pentaho
