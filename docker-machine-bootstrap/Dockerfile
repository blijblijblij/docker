FROM debian:stable

MAINTAINER Rogier Wessel <rhwessel@xs4all.nl>

RUN apt-get update && \
    apt-get install -y ansible ssh && \
    rm -rf /var/lib/apt/lists/*

ADD ./machine.py /machine.py
ADD ./playbooks /playbooks
ADD ./conf/ansible.cfg /etc/ansible/ansible.cfg
ADD ./entrypoint.sh /entrypoint.sh

ENTRYPONT ["./entrypoint.sh"]

CMD ["/playbooks/bootstrap.yml"]
