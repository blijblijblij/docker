FROM blijblijblij/base:latest

MAINTAINER Rogier Wessel, rhwessel@xs4all.nl

# add webupd8 repository
RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee /etc/apt/sources.list.d/webupd8team-java.list 
RUN echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886  

RUN apt-get update  

RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections
RUN apt-get install -y --force-yes oracle-java8-installer oracle-java8-set-default

RUN rm -rf /var/cache/oracle-jdk7-installer && apt-get clean && rm -rf /var/lib/apt/lists/*
