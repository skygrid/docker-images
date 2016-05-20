FROM ubuntu:14.04

RUN echo "nameserver 2a02:6b8:0:3400::1023" > /etc/resolv.conf
RUN apt-get update
RUN apt-get -y  install nginx python-virtualenv python-dev build-essential libevent-dev python-all-dev git

RUN mkdir /opt/metascheduler
RUN virtualenv /opt/metascheduler/venv
RUN /opt/metascheduler/venv/bin/pip install git+https://github.com/skygrid/metascheduler.git
RUN /opt/metascheduler/venv/bin/pip install gunicorn

ADD configs /opt/metascheduler/configs
ADD metascheduler /opt/metascheduler/bin/metascheduler