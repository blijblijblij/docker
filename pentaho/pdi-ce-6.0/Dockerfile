FROM blijblijblij/java:8

MAINTAINER Rogier Wessel, rhwessel@xs4all.nl

ENV MAJOR_VERSION 6.0
ENV MINOR_VERSION 6.0.0.0-353

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

# add libs
ADD mysql-connector-java-5.1.18.jar /opt/pentaho/data-integration/lib/mysql.jar
ADD postgresql-9.1-901.jdbc4.jar /opt/pentaho/data-integration/lib/postgresql.jar
ADD vertica-jdk5-6.1.2-0.jar /opt/pentaho/biserver-ce/tomcat/lib/vertica.jar

ENTRYPOINT ["/bin/bash"]

USER pentaho
