FROM ubuntu:latest

MAINTAINER Colin But colin.but@outlook.com

RUN apt-get update
RUN apt-get install -y wget

RUN echo "Installing Jenkins"
RUN wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
RUN sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
RUN apt-get update
RUN apt-get install -y jenkins
RUN sed -i 's/8080/6060/g' /etc/default/jenkins
RUN mkdir -p /var/run/jenkins/
RUN /etc/init.d/jenkins restart


