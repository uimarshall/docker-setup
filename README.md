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

## DOCKERIZE A REACT APP

> STEPS
> Run the following commands

```
npm create vite@latest dockerize-react
```

Follow prompt.

- Choose the flavour of JavaScript you want (React).
- Choose the variant (Typescript).

Build the image

```
docker build -t dockerize-react .
```

Containerize the app

```
docker run dockerize-react
```

Since docker run in an isolated environment, i.e. the port EXPOSED is only available to the docker container but not exposed to the host machine.

To expose to the host machine, we map the port exposed in the `Dockerfile` to the machine with the command below:

```
docker run -p 5173:5173 dockerize-react
```

`dockerize-react` as appended at the end of the command, tells which image to run.

Automate changes in the app

```
docker run -p 5173:5173 -v "$(pwd):/app" -v /app/node_modules dockerize-react
```

`$(pwd):/app` - This will tell docker to Mount the current working directory where we run the docker `RUN` command, onto the `/app` directory inside the container.

This will make our local changes to the code to immediately reflect in the running container.

The below command works for windows:

```
docker run -p 5173:5173 -v %cd%:/app -v /app/node_modules dockerize-react
```

Or use `CURDIR`

```
docker run -p 5173:5173 -v "${CURDIR}":/app -v /app/node_modules dockerize-react
```

Publish the image

```
docker login
```

```
docker tag dockerize-react uimarshall/dockerize-react
```

Push to docker hub

```
docker push uimarshall/dockerize-react
```

## AUTOMATE PROCESS USING DOCKER COMPOSE

Docker compose is a tool that help us to `Define` and `Manage` a `multi-container` docker applications.

It uses a `yml` file to configure `Services`, `Networks` and `Volumes` for our application. Enabling us to run and scale the application with a single command (`docker compose up`).

```
npm create vite@latest vite-project
```

```
cd vite-project
```

Create `yml` file.

```
docker init
```

Follow prompt to answer the below questions.

- Choose `Node` as application platform or your choice depending on tech stack.
- Choose `version`.
- Choose `npm`.
- Choose `No` to `run npm build` before starting your server.
- Use `npm run dev` to start the app as a choice command.
- Specify the port.

On windows, open your terminal as administrator to avoid `Access denied`

```
docker compose up
```

On linux

```
sudo docker compose up
```

Automate changes in the code

```
docker compose watch
```

The `docker compose watch` listen to changes in our app or code and performs operations such as

- Re-building the app
- Re-running the container

It does the following🧮

- sync
- rebuild
- sync-restart
