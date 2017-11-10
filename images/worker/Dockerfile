FROM centos:7

# Install xrootd
RUN rpm -Uvh http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

RUN yum install -y gcc python-devel xrootd xrootd-client xrootd-client-devel xrootd-python git xrootd-server 

RUN yum install -y python-pip

RUN adduser --uid 1001 xrootduser

RUN pip install git+https://github.com/andreiSaw/pydisneyland
RUN pip install git+https://github.com/sashabaranov/easywebdav
RUN pip install git+https://github.com/skygrid/hep-data-backends
RUN git clone https://github.com/andreiSaw/docker-worker /src/docker-worker/source/
RUN pip install git+https://github.com/andreiSaw/docker-worker
RUN pip install parse
ADD docker-worker /src/docker-worker/bin/docker-worker

# Make port 80 available to the world outside this container
EXPOSE 80

# Copy the current directory contents into the container at
ADD .disney /src/docker-worker/.disney

# Define environment variables
ENV DOCKER_WORKER_CONFIG /src/docker-worker/.disney/worker.cfg
ENV DISNEYLAND_CLIENT_CONFIG /src/docker-worker/.disney/config.yml

# print xrootd version
RUN xrootd -v
# Run run.py when the container launches
CMD python /src/docker-worker/source/run.py
