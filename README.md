# docker-setup

This repository is for docker setup

## DOCKER WORKFLOW

- Docker Client
  This is the user interface for interacting with docker.
- Docker Host (Docker Daemon)
  This is the background process responsible for managing processes on the host system.
  It listens to docker client commands, Creates and manages containers and handles other docker related tasks.
- Docker Registry (Docker Hub)
  This is where the docker images are stored. It functions more like Github.

## DOCKER COMMANDS

`RUN` - Executes command in the shell during image build.

`EXPOSE` - Tells docker which port to listen to at runtime.

`ENV` - Sets the environment variable during build process.

`ARG` - Defines the build time variable.

```
ARG NODE_VERSION = 21
```

`VOLUME` - Specifies a point in your container where you can connect external storage.

`CMD` - Defines the full command to be executed when the container starts.

```
CMD ["npm", "run", "dev"]
```

`ENTRYPOINT` - Determines the default executables to be run when the container starts. Entrypoint commands cannot be overridden, but CMD commands can be overridden.

```
CMD npm run dev
```
