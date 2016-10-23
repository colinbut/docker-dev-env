FROM ubuntu:latest

MAINTAINER Colin But <colin.but@outlook.com>

RUN apt-get update
RUN apt-get install -y wget
RUN apt-get install -y unzip

# Java
RUN echo "Installing Java 8"
RUN apt-get install -y software-properties-common python-software-properties
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN add-apt-repository ppa:webupd8team/java -y
RUN apt-get update
RUN apt-get install -y oracle-java8-installer
RUN echo "Setting environment variables for Java 8"
RUN apt-get install -y oracle-java8-set-default

# Maven
RUN echo "Installing Maven"
RUN apt-get install -y maven
RUN echo "Finished installing Maven"

# Git
RUN echo "Installing Git"
RUN apt-get install -y git
RUN echo "Finished installing Git"

# Jenkins
RUN echo "Installing Jenkins"
RUN wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
RUN sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
RUN apt-get update
RUN apt-get install -y jenkins
RUN sed -i 's/8080/6060/g' /etc/default/jenkins
RUN mkdir -p /var/run/jenkins/
RUN /etc/init.d/jenkins restart
RUN echo "Finished installing Jenkins"

# SonarQube Server
RUN echo "Downloading Sonar"
RUN echo "Installing Sonar"
RUN wget https://sonarsource.bintray.com/Distribution/sonarqube/sonarqube-5.5.zip
RUN unzip sonarqube-5.5.zip
RUN mv -v sonarqube-5.5 /opt/sonar
RUN /opt/sonar/bin/linux-x86-64/sonar.sh start
RUN echo "Finished installing Sonar"

# Sonar Runner
RUN echo "Installing Sonar Runner"
RUN cd /opt
RUN wget http://repo1.maven.org/maven2/org/codehaus/sonar/runner/sonar-runner-dist/2.4/sonar-runner-dist-2.4.zip
RUN unzip sonar-runner-dist-2.4.zip
RUN ln -s sonar-runner-2.4 sonar-runner
RUN echo "Finished installing Sonar Runner"

# Nexus Repository
RUN echo "Downloading Nexus"
RUN echo "Installing Nexus"
RUN cd /usr/local/
RUN wget www.sonatype.org/downloads/nexus-2.13.0-01-bundle.zip
RUN echo "Extracting Nexus"
RUN unzip nexus-2.13.0-01-bundle.zip
RUN ln -s nexus-2.13.0-01 nexus
RUN echo "Adding Nexus User"
RUN useradd nexus
RUN chown -R nexus:nexus nexus
RUN chown -R nexus:nexus nexus-2.13.0-01
RUN chown -R nexus:nexus sonatype-work
RUN echo "Configuring Nexus script to have correct environment properties"
RUN sed -i 's/NEXUS_HOME=".."/NEXUS_HOME="\/usr\/local\/nexus"/g' /usr/local/nexus/bin/nexus
RUN sed -i 's/#RUN_AS_USER=/RUN_AS_USER=nexus/' /usr/local/nexus/bin/nexus
RUN echo "Removing nexus download zip"
RUN rm nexus-2.13.0-01-bundle.zip
RUN echo "Starting Nexus"
RUN /usr/local/nexus/bin/nexus start
RUN echo "Finished installing Nexus"

# MySQL
RUN echo "Installing MySQL"
RUN apt-get install -y debconf-utils
RUN debconf-set-selections <<< "mysql-server mysql-server/root_password password root"
RUN debconf-set-selections <<< "mysql-server mysql-server/root_password_again password root"
RUN apt-get install -y mysql-server
RUN echo "Finished installing MySQL"

# Apache Httpd Web Server
RUN echo "Installing Apache"
RUN apt-get install -y apache2
RUN echo "Finished installing Apache"

# NGINX
RUN echo "Installing NGINX"
RUN apt-get install -y nginx
RUN /etc/init.d/nginx start &
RUN echo "Finished installing NGINX"

# MongoDB
RUN echo "Installing MongoDB"
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
RUN echo "deb http://repo.mongodb.org/apt/ubuntu "$(cat /etc/lsb-release | grep DISTRIB_CODENAME | cut -d= -f2)"/mongodb-org/3.2 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-3.2.list
RUN apt-get clean
RUN apt-get update && apt-get install -y mongodb-org
#RUN apt-get install -y mongodb-org
#RUN apt-get install -y mongodb-org-server
#RUN apt-get install -y mongodb-org-shell
#RUN apt-get install -y mongodb-org-mongos
#RUN apt-get install -y mongodb-org-tools
RUN mkdir -p /data/db
EXPOSE 27017
RUN echo "Finished installing MongoDB"

# Tomcat
RUN echo "Installing Tomcat"
RUN apt-get install -y tomcat7
RUN echo "Installing Tomcat docs"
RUN apt-get install -y tomcat7-docs
RUN echo "Installing Tomcat administration web apps"
RUN apt-get install -y tomcat7-admin
RUN echo "Installing Tomcat examples"
RUN apt-get install -y tomcat7-examples
RUN echo "Finished installing Tomcat"
