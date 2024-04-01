# Creating Docker Images

FROM node:20-alpine

# The directory from where the commands will be executed

WORKDIR /app

# Copy everything from the current directory to the docker image

COPY . .

# Specify the command to run the app or when the container starts 

CMD node welcome.js

# Use the command below to run the app in the terminal:
# docker build -t hello-docker . - To build the container image. The -t flag is used to tag the image with a name. The . is the path to the Dockerfile.
# docker run hello-docker - To run the container in the terminal, this is the image we just created. And this is what we mean by containerizing the app.

