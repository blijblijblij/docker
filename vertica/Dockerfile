FROM ubuntu:14.04
MAINTAINER Sumit Chawla <sumitkchawla@gmail.com>

# Update the image
RUN apt-get update -y && apt-get upgrade -y

# Install Dependencies
RUN apt-get install -y openssh-server openssh-client mcelog gdb sysstat

# grab gosu for easy step-down from root
RUN apt-get install -y curl \
	&& curl -o /usr/local/bin/gosu -SL 'https://github.com/tianon/gosu/releases/download/1.1/gosu' \
	&& chmod +x /usr/local/bin/gosu

RUN apt-get clean

# Set locale for all system
RUN locale-gen en_US en_US.UTF-8
RUN dpkg-reconfigure locales

# Vertica requires bash as default shell
ENV SHELL "/bin/bash"

# Create user dbadmin and configure it
RUN groupadd -r verticadba
RUN useradd -r -m -g verticadba dbadmin
RUN chsh -s /bin/bash dbadmin
RUN chsh -s /bin/bash root
RUN echo "dbadmin -       nice    0" >> /etc/security/limits.conf
RUN echo "dbadmin -       nofile  65536" >> /etc/security/limits.conf

# Install package
ADD vertica_7.1.2-0_amd64.deb /tmp/vertica.deb
RUN dpkg -i /tmp/vertica.deb

# In theory, someone should make things work without ignoring the errors.
# But that's in theory, and for now, this seems sufficient.
RUN /opt/vertica/sbin/install_vertica --license CE --accept-eula --hosts 127.0.0.1 --dba-user-password-disabled --failure-threshold NONE --no-system-configuration

# Test DB creation as dbuser
USER dbadmin
RUN /opt/vertica/bin/admintools -t create_db -s localhost -d docker -c /home/dbadmin/docker/catalog -D /home/dbadmin/docker/data

USER root

RUN mkdir /tmp/.python-eggs
RUN chown -R dbadmin /tmp/.python-eggs
ENV PYTHON_EGG_CACHE /tmp/.python-eggs

ENV VERTICADATA /home/dbadmin/docker
VOLUME  /home/dbadmin/docker

# Starts Vertice after run and finishes it
ADD docker-entrypoint.sh /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 5433

RUN chmod +x /docker-entrypoint.sh
