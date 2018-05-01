# Docker

We use Docker to manage dev, test, stage and prod environments. Specific conventions we follow:

  * It should be as easy and quick as possible to set up a new environment.
  * production and development environments should be as similar as possible (or, as practical anyway).
  * Base your Dockerfiles on official dockerhub.com images where they exist.
  * docker-compose.yml contains the Docker config which is the same between every environment.
  * A file called docker-compose.override.yml.template should exist with any settings that vary between environments. In a particular environment, to set up you would copy it and modify it locally. docker-compose.override.yml should be in `.gitignore`
  * The docker-compose.override.yml file should only contain differences between dev and prod and other environments. This includes the ports, restart policy, and normally not much else. If a line doesn't need to be in the overrides for a specific reason, move it to the main docker-compose.yml instead.

## Setting Up An Environment

1. [Install Docker on your machine](https://docs.docker.com/engine/installation/)

2. Clone one of our beautiful apps.

3. Copy the docker override template: `cp docker-compose.override.yml.template docker-compose.override.yml`

4. Run docker-compose: `docker-compose up`

5. Navigate to http://localhost.

6. If you want to use a different port on the host, such as when you want to run environments on the same host, map that in docker-compose.override.yml

```
services:
  web:
    ports:
      -9000:80
```

And visit http://localhost:9000