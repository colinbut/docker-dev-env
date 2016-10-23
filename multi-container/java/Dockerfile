FROM ubuntu:latest

MAINTAINER Colin But colin.but@outlook.com

RUN apt-get update

RUN echo "Installing Java 8"
RUN apt-get install -y software-properties-common python-software-properties
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN add-apt-repository ppa:webupd8team/java -y
RUN apt-get update
RUN apt-get install -y oracle-java8-installer
RUN echo "Setting environment variables for Java 8"
RUN apt-get install -y oracle-java8-set-default 
