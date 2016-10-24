# Docker Development Environment

A docker container image for MongoDB

To use, just build the docker image

To build the image:

docker build --tag [your repo]/[image name] .
To run the container:

docker run -d [your repo]/[image name]
Can use image as a base for other applications that runs on Unix/Linux environments.

In your Dockerfile (first line)

FROM [your repo]/[image name]
ideally, you would have built your image and uploaded to a Docker Registry (either a private hosted docker registry or Docker Hub).
