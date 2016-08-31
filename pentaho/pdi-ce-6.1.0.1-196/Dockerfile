FROM blijblijblij/java:8

MAINTAINER Rogier Wessel, rhwessel@xs4all.nl

ENV MAJOR_VERSION 6.0
ENV MINOR_VERSION 6.0.1.0-386

# Update the APT cache
RUN apt-get update && apt-get upgrade -y

# Set up Pentaho user + directory
RUN useradd -m pentaho
RUN mkdir /opt/pentaho
RUN chown pentaho:pentaho /opt/pentaho

RUN su -c "curl -L http://downloads.sourceforge.net/project/pentaho/Data%20Integration/$MAJOR_VERSION/pdi-ce-$MINOR_VERSION.zip \
  -o /opt/pentaho/pdi-ce.zip && \
  unzip -q /opt/pentaho/pdi-ce.zip \
  -d /opt/pentaho/ && \
  rm -f /opt/pentaho/pdi-ce.zip" pentaho

# Add libs
ADD lib/mysql-connector-java-5.1.35-bin.jar /opt/pentaho/biserver-ce/tomcat/lib/mysql.jar
ADD lib/vertica-jdbc-7.2.3-0.jar /opt/pentaho/biserver-ce/tomcat/lib/vertica.jar

ENTRYPOINT ["/bin/bash"]

USER pentaho