FROM ubuntu:latest

MAINTAINER Colin But <colin.but@outlook.com>

RUN apt-get update
RUN echo "Installing Apache"
RUN apt-get install -y apache2

ENTRYPOINT["service","apache2","start"]

