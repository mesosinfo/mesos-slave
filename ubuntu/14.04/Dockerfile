# DOCKER-VERSION 1.9.1
# VERSION        0.1
# SOURCE         https://github.com/mesosinfo/mesos-slave

FROM ubuntu:14.04
MAINTAINER Yong Zhang<zhangyong.net@qq.com>

# Install dependancies
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv E56151BF && \
echo deb http://repos.mesosphere.io/ubuntu trusty main > /etc/apt/sources.list.d/mesosphere.list && \
apt-get update
RUN sudo apt-get -y install curl python-setuptools python-pip python-dev python-protobuf

# Install mesos.
RUN sudo apt-get -y install mesos
RUN sudo mkdir -p /etc/mesos-slave

# http://docs.docker.com/installation/ubuntulinux/
RUN curl -fLsS https://get.docker.com/ | sh

CMD ["/usr/sbin/mesos-slave"]

#ENV MESOS_WORK_DIR /etc/mesos-slave
#ENV MESOS_CONTAINERIZERS docker,mesos

# https://mesosphere.github.io/marathon/docs/native-docker.html
#ENV MESOS_EXECUTOR_REGISTRATION_TIMEOUT 5mins

VOLUME /etc/mesos-slave

ENTRYPOINT ["mesos-slave"]
