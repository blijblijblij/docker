FROM blijblijblij/java:7

MAINTAINER Rogier Wessel <rhwessel@xs4all.nl>

# Set the env variables to non-interactive
ENV DEBIAN_FRONTEND noninteractive
ENV DEBIAN_PRIORITY critical
ENV DEBCONF_NOWARNINGS yes
ENV JAVA_HOME /usr/lib/jvm/java-7-oracle/

# make sure the package repository is up to date
RUN echo "deb http://ftp.nl.debian.org/debian stable main contrib non-free" > /etc/apt/sources.list
RUN echo "deb http://ftp.debian.org/debian/ wheezy-updates main contrib non-free" >> /etc/apt/sources.list
RUN echo "deb http://security.debian.org/ wheezy/updates main contrib non-free" >> /etc/apt/sources.list

# update && install packages
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y --force-yes --no-install-recommends wget unzip sudo

ADD setup-agent.sh /setup-agent.sh
RUN useradd -m teamcity

EXPOSE 9090

CMD sudo -u teamcity -s -- sh -c "TEAMCITY_SERVER=$TEAMCITY_SERVER bash /setup-agent.sh run"
