FROM blijblijblij/java:7

MAINTAINER Rogier Wessel <rhwessel@xs4all.nl>

# Define variables
ENV JAVA_HOME /usr/lib/jvm/java-7-oracle/
ENV TEAMCITY_DATA_PATH /data/teamcity
ENV TEAMCITY_DOWNLOAD http://download.jetbrains.com/teamcity
ENV TEAMCITY_PACKAGE TeamCity-9.0.4.tar.gz
ENV POSTGRES_DOWLOAD https://jdbc.postgresql.org/download
ENV POSTGRES_PACKAGE postgresql-9.4-1201.jdbc41.jar

# TeamCity data is stored in a volume to facilitate container upgrade
VOLUME  ["/data/teamcity"]

# Download and install TeamCity to /opt
RUN wget -q $TEAMCITY_DOWNLOAD/$TEAMCITY_PACKAGE && tar zxf $TEAMCITY_PACKAGE -C /opt && rm -rf $TEAMCITY_PACKAGE

# Download the postgres driver
RUN mkdir $TEAMCITY_DATA_PATH/lib && mkdir $TEAMCITY_DATA_PATH/lib/jdbc/ && wget -q https://jdbc.postgresql.org/download/postgresql-9.4-1201.jdbc41.jar -o $TEAMCITY_DATA_PATH/lib/jdbc/postgres.jar

# Expose teamcity via port 8111
EXPOSE 8111

CMD ["/opt/TeamCity/bin/teamcity-server.sh", "run"]

# Define working directory.
WORKDIR /data
