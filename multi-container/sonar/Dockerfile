FROM ubuntu:latest

MAINTAINER Colin But colin.but@outlook.com

RUN apt-get update
RUN apt-get install -y wget
RUN apt-get install -y unzip

RUN echo "Installing Java 8"
RUN apt-get install -y software-properties-common python-software-properties
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN add-apt-repository ppa:webupd8team/java -y
RUN apt-get update
RUN apt-get install -y oracle-java8-installer
RUN echo "Setting environment variables for Java 8"
RUN apt-get install -y oracle-java8-set-default

RUN echo "Downloading Sonar"
RUN wget https://sonarsource.bintray.com/Distribution/sonarqube/sonarqube-5.5.zip
RUN unzip sonarqube-5.5.zip
RUN mv -v sonarqube-5.5 /opt/sonar
RUN /opt/sonar/bin/linux-x86-64/sonar.sh start

# Sonar Runner
RUN cd /opt
RUN wget http://repo1.maven.org/maven2/org/codehaus/sonar/runner/sonar-runner-dist/2.4/sonar-runner-dist-2.4.zip
RUN unzip sonar-runner-dist-2.4.zip
RUN ln -s sonar-runner-2.4 sonar-runner
