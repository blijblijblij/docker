FROM blijblijblij/java:7

MAINTAINER Rogier Wessel, rhwessel@xs4all.nl

RUN apt-get update && apt-get upgrade -y

# Set up Pentaho user + directory
# - must have home directory where Pentaho can store config etc
# - also set up installation directory with ownership
RUN useradd -m pentaho
RUN mkdir /opt/pentaho
RUN chown pentaho:pentaho /opt/pentaho

# possible biserver downloads
# http://sourceforge.net/projects/pentaho/files/Business%20Intelligence%20Server/5.2/biserver-ce-5.2.0.0-209.zip/download
# http://sourceforge.net/projects/pentaho/files/Business%20Intelligence%20Server/5.1/biserver-ce-5.1.0.0-752.zip/download
# http://sourceforge.net/projects/pentaho/files/Business%20Intelligence%20Server/5.0.1-stable/biserver-ce-5.0.1-stable.zip/download
# Install Pentaho Business Analytics
RUN su -c "curl -L http://sourceforge.net/projects/pentaho/files/Business%20Intelligence%20Server/5.2/biserver-ce-5.2.0.0-209.zip/download -o /opt/pentaho/biserver-ce.zip && unzip -q /opt/pentaho/biserver-ce.zip -d /opt/pentaho/ && rm -f /opt/pentaho/biserver-ce.zip" pentaho

# Disable first-time startup prompt
RUN rm /opt/pentaho/biserver-ce/promptuser.sh
# Disable daemon mode for Tomcat
RUN sed -i -e 's/\(exec ".*"\) start/\1 run/' /opt/pentaho/biserver-ce/tomcat/bin/startup.sh

# add libs
ADD mysql-connector-java-5.1.18.jar /opt/pentaho/biserver-ce/tomcat/lib/mysql.jar

# Set up runtime options
EXPOSE 8080

ENTRYPOINT ["/opt/pentaho/biserver-ce/start-pentaho.sh"]

USER pentaho
