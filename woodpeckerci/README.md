# Woodpecker CI

Before you start, know that because every built is done inside of docker, it is VERY complicated to deploy a docker compose project through this method. The way I achieved it here was by doing the following:

- Use the docker base image
- Mount the host docker socket inside the image so when a docker command is ran inside the container, it actually uses the host docker socket
- Create an image for every container during building, bind mounts do not work because the container that is used to deploy the application is destroyed after the build is complete, any mounted files will be destroyed alongside it. Hence why we copy over the files we normally mount inside the image.
- Run `docker compose up --build -d` inside the container

## Installation
Fill in a `.env` with the variables from the `.example.env` file. Below a quick explanation can be found:

- WOODPECKER_HOST: The hostname where woodpecker will be accessible from
- WOODPECKER_AGENT_SECRET: The secret used for communication between woodpecker and the docker agent
- WOODPECKER_GITHUB_CLIENT: The client of the github oauth2 application
- WOODPECKER_GITHUB_SECRET: The secret of the github oauth2 application
- ADMIN_ACCOUNTS: the username(s) of the administration account used to login with.

## Usage
Login with the admin account, add a repository and go into it's settings, then in the project settings, enable the trusted checkbox so the pipeline can mount host files into it's container. Next, create a `.woodpecker/deploy.yaml` file inside the repository, this will be the file that contains the pipeline. Below is an example pipeline used for deploying:
```yaml
steps:
  build:
    image: docker:20.10.16
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    commands:
      - "docker compose up --build -d"
    secrets:
      - DB_USR
      - DB_PW
      - DB_DATABASE
      - DB_ROOT_PW
```
I have created secrets inside the repository settings on woodpecker, these secrets are passed as environmental variables when the build pipeline is ran. Again, do note that you need to create a docker image if you're bind mounting files and copy them over instead!