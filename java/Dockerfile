# AMEE java developer environment
# License: GPL-3.0

FROM phusion/baseimage:0.10.1
MAINTAINER Simome Rotondo <simone.rotondo@gmail.com>

# Set environment variables
ENV DEBIAN_FRONTEND noninteractive
ENV HOME /root
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8

WORKDIR /root

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# Install prerequisites
RUN apt update && \
    apt install -y vim sudo curl wget netcat-openbsd git openjdk-8-jdk-headless maven

# Clean up APT when done
RUN apt clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Create fs structure
RUN bash -c 'mkdir -pv /opt/amee/dev'

# Configure JAVA
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
ENV PATH=${PATH}:/usr/lib/jvm/java-8-openjdk-amd64/bin

WORKDIR "/opt/amee/dev/"
