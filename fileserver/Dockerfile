FROM gliderlabs/alpine:3.1

MAINTAINER Rogier Wessel, rhwessel@xs4all.nl

RUN apk-install python && mkdir /share

WORKDIR /share

VOLUME ["/share"]

CMD python -m SimpleHTTPServer 5000

EXPOSE 5000
