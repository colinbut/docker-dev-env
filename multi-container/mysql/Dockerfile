FROM ubuntu:latest

MAINTAINER Colin But colin.but@outlook.com

RUN apt-get update

RUN echo "Installing MySQL Server"
RUN apt-get install -y debconf-utils
RUN debconf-set-selections <<< "mysql-server mysql-server/root_password password root"
RUN debconf-set-selections <<< "mysql-server mysql-server/root_password_again password root"
RUN apt-get install -y mysql-server
