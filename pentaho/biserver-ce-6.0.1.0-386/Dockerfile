FROM blijblijblij/java:8

MAINTAINER Rogier Wessel, rhwessel@xs4all.nl

ENV MAYOR_VERSION 6.0
ENV MINOR_VERSION 6.0.1.0-386

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
ADD https://github.com/blijblijblij/docker/raw/develop/lib/mysql-connector-java-5.1.35-bin.jar /opt/pentaho/biserver-ce/tomcat/lib/mysql.jar
ADD https://github.com/blijblijblij/docker/raw/develop/lib/postgresql-9.4-1201.jdbc41.jar /opt/pentaho/biserver-ce/tomcat/lib/postgres.jar
ADD https://github.com/blijblijblij/docker/raw/develop/lib/vertica-jdbc-7.2.3-0.jar /opt/pentaho/biserver-ce/tomcat/lib/vertica.jar

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
