# DOCKER-VERSION 1.10.3
# VERSION        0.1
# SOURCE         https://github.com/mesosinfo/mesos-slave

FROM ubuntu:14.04
MAINTAINER Yong Zhang<zhangyong.net@qq.com>

# Install dependancies
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv E56151BF && \
echo deb http://repos.mesosphere.io/ubuntu trusty main > /etc/apt/sources.list.d/mesosphere.list && \
apt-get update
RUN sudo apt-get -y install curl python-setuptools python-pip python-dev python-protobuf

# http://docs.docker.com/installation/ubuntulinux/
RUN curl -fLsS https://get.docker.com/ | sh

# Install mesos.
RUN sudo apt-get -y install mesos=0.28.0-2.0.16.ubuntu1404
RUN sudo mkdir -p /etc/mesos-slave

ENTRYPOINT ["mesos-slave"]
