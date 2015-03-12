FROM blijblijblij/java:7

MAINTAINER Rogier Wessel, rhwessel@xs4all.nl

# Update the APT cache
RUN apt-get update && apt-get upgrade -y

# Set up Pentaho user + directory
RUN useradd -m pentaho
RUN mkdir /opt/pentaho
RUN chown pentaho:pentaho /opt/pentaho

# Install pdi

RUN su -c "curl -L http://sourceforge.net/projects/pentaho/files/Data%20Integration/5.3/pdi-ce-5.3.0.0-213.zip/download -o /opt/pentaho/pdi-ce.zip && unzip -q /opt/pentaho/pdi-ce.zip -d /opt/pentaho/ && rm -f /opt/pentaho/pdi-ce.zip" pentaho

# add libs
ADD mysql-connector-java-5.1.18.jar /opt/pentaho/data-integration/lib/mysql.jar
ADD postgresql-9.1-901.jdbc4.jar /opt/pentaho/data-integration/lib/postgresql.jar

ENTRYPOINT ["/bin/bash"]

USER pentaho
