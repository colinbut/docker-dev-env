FROM ubuntu:latest

MAINTAINER Colin But colin.but@outlook.com

RUN apt-get update
RUN apt-get install -y wget
RUN apt-get install -y unzip

RUN echo "Downloading Nexus"
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


