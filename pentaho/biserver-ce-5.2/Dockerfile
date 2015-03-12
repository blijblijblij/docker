FROM blijblijblij/java:7

MAINTAINER Rogier Wessel, rhwessel@xs4all.nl

# Set up Pentaho user + directory
RUN useradd -m pentaho
RUN mkdir /opt/pentaho
RUN chown pentaho:pentaho /opt/pentaho

# Install Pentaho Business Analytics
RUN su -c "curl -L http://sourceforge.net/projects/pentaho/files/Business%20Intelligence%20Server/5.2/biserver-ce-5.2.0.0-209.zip/download -o /opt/pentaho/biserver-ce.zip && unzip -q /opt/pentaho/biserver-ce.zip -d /opt/pentaho/ && rm -f /opt/pentaho/biserver-ce.zip" pentaho

# Disable first-time startup prompt
RUN rm /opt/pentaho/biserver-ce/promptuser.sh
# Disable daemon mode for Tomcat
RUN sed -i -e 's/\(exec ".*"\) start/\1 run/' /opt/pentaho/biserver-ce/tomcat/bin/startup.sh

# Add libs
ADD mysql-connector-java-5.1.18.jar /opt/pentaho/biserver-ce/tomcat/lib/mysql.jar
ADD postgresql-9.1-901.jdbc4.jar /opt/pentaho/biserver-ce/tomcat/lib/postgresql.jar

# Set up runtime options
EXPOSE 8080

ENTRYPOINT ["/opt/pentaho/biserver-ce/start-pentaho.sh"]

USER pentaho
