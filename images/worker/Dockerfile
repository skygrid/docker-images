FROM centos:7

# Install xrootd
RUN yum -y --nogpg update
# Add required repositories
ADD *.repo /etc/yum.repos.d/

RUN yum install -y gcc python-devel xrootd xrootd-client xrootd-client-devel xrootd-python git
RUN yum install -y python-pip

# print xrootd version
RUN xrootd -v

RUN mkdir /opt/docker-worker
RUN pip install git+https://github.com/andreiSaw/pydisneyland
RUN pip install git+https://github.com/sashabaranov/easywebdav
RUN pip install git+https://github.com/skygrid/hep-data-backends
RUN pip install git+https://github.com/andreiSaw/docker-worker

ADD docker-worker /opt/docker-worker/bin/docker-worker
ADD configs /opt/docker-worker/configs
ADD .disney /root/.disney
ENV DOCKER_WORKER_CONFIG=/opt/docker-worker/configs/worker.cfg
CMD bin/bash ./opt/docker-worker/bin/docker-worker
