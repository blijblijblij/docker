FROM blijblijblij/base:latest

MAINTAINER Rogier Wessel, rhwessel@xs4all.nl

RUN apt-get update  

#Install CLIs

RUN apt-get update && apt-get install -y python-pip && pip install awscli

RUN apt-get clean && rm -rf /var/lib/apt/lists/*
