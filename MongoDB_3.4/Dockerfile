#
# MongoDB Dockerfile in CentOS 7 image
#

# Build:
# docker build -t winslow90/mongodb:latest .
#
# Create:
# docker create -it -p 27017:27017 --name mongodb winslow90/mongodb
#
# Start:
# docker start mongodb
#
# Connect with mongo
# docker exec -it mongodb mongo
#
# Connect bash
# docker exec -it mongodb bash


# Pull base image
FROM centos:centos7

# Maintener
MAINTAINER Wentao Li <liwentao90@yahoo.com>

# Install MongoDB
RUN echo -e "[mongodb-org-3.4]\nname=MongoDB Repository\nbaseurl=https://repo.mongodb.org/yum/redhat/7/mongodb-org/3.4/`uname -m`/\ngpgcheck=1\nenabled=1\ngpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc" > /etc/yum.repos.d/mongodb.repo && \
    yum install -y mongodb-org && \
    yum clean all && \
    chown -R mongod:mongod /var/lib/mongo

RUN mkdir -p /data/db 

RUN chown -R mongod:mongod /data/db

# User
USER mongod

# Mountable directories
VOLUME ["/var/lib/mongo"]

# Set the environment variables
ENV HOME /var/lib/mongo

# Working directory
WORKDIR /var/lib/mongo

ENTRYPOINT ["/bin/mongod"]

# Expose ports.
EXPOSE 27017
