# use the debian stable as my base image

FROM debian:stable

MAINTAINER Rogier Wessel, rhwessel@xs4all.nl

# Set the env variables to non-interactive
ENV DEBIAN_FRONTEND noninteractive
ENV DEBIAN_PRIORITY critical
ENV DEBCONF_NOWARNINGS yes

# make sure the package repository is up to date
RUN echo "deb http://ftp.nl.debian.org/debian stable main contrib non-free" > /etc/apt/sources.list
RUN echo "deb http://ftp.debian.org/debian/ wheezy-updates main contrib non-free" >> /etc/apt/sources.list
RUN echo "deb http://security.debian.org/ wheezy/updates main contrib non-free" >> /etc/apt/sources.list

# update && install packages
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y --force-yes --no-install-recommends ca-certificates software-properties-common
RUN apt-get install -y --force-yes --no-install-recommends curl git git-flow htop less mc nload ssh tmux unzip vim wget zip

USER root
