# Dockerizing MongoDB: Dockerfile for building MongoDB images
# Based on ubuntu:latest, installs MongoDB following instructions from:
# http://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/

FROM ubuntu:16.04

MAINTAINER Colin But colin.but@outlook.com

# Importing MongoDB public GPG key AND create a MongoDB list file
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
RUN echo "deb http://repo.mongodb.org/apt/ubuntu "$(cat /etc/lsb-release | grep DISTRIB_CODENAME | cut -d= -f2)"/mongodb-org/3.2 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-3.2.list

# Installation
RUN apt-get clean
RUN apt-get update && apt-get install -y mongodb-org

#RUN apt-get install -y mongodb-org
#RUN apt-get install -y mongodb-org-server 
#RUN apt-get install -y mongodb-org-shell 
#RUN apt-get install -y mongodb-org-mongos 
#RUN apt-get install -y mongodb-org-tools

# Creating the MongoDB data directory
RUN mkdir -p /data/db

EXPOSE 27017

ENTRYPOINT ["/usr/bin/mongod"]



