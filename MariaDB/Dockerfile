#
# MariaDB Dockerfile in CentOS 7 image
#

# Build:
# docker build --rm -t winslow90/mariadb55:latest .
#
# Create:
# docker run -p 3306:3306 --name=mariadb5501 -e MYSQL_ROOT_PASSWORD=password -d winslow90/mariadb55
#
# Start:
# docker start mariadb
#
# Connect with mongo
# docker exec -it mariadb5501
#
# Connect bash
# docker exec -it mariadb5501 bash


FROM centos:centos7

MAINTAINER Wentao Li <liwentao90@yahoo.com>

RUN yum -y install --setopt=tsflags=nodocs epel-release && \ 
    yum -y install --setopt=tsflags=nodocs mariadb-server bind-utils pwgen psmisc hostname && \ 
    yum -y erase vim-minimal && \
    yum -y update && yum clean all


# Fix permissions to allow for running on openshift
COPY fix-permissions.sh ./

RUN chmod +x ./fix-permissions.sh

RUN ./fix-permissions.sh /var/lib/mysql/   && \
    ./fix-permissions.sh /var/log/mariadb/ && \
    ./fix-permissions.sh /var/run/

COPY docker-entrypoint.sh /

RUN chmod +x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]

# Place VOLUME statement below all changes to /var/lib/mysql
VOLUME /var/lib/mysql

# By default will run as random user on openshift and the mysql user (27)
# everywhere else
USER 27

EXPOSE 3306
CMD ["mysqld_safe"]
