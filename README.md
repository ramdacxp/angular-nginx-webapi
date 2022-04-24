# Angular NGINX WebAPI setup for Docker Compose

This cheat sheet repo contains my reference `Dockerfile`s and configuration to setup a project containing:

* Angular app
  * Build in Docker
  * Host via NGINX webserver in Docker Container
* WebAPI
  * Provided by DotNet 6 Kestrel webserver
  * Executed in Docker container
* Docker Compose
  * Build and hosting of all containers
  * WebAPI NGINX reverse proxy for container network
  * Portainer compose setup

## Angular SPA

Requires [Node LTS](https://nodejs.org/en/) and Angular CLI (`npm i -g @angular/cli`).

Create via:

```cmd
ng new --routing --skip-tests --style=scss client
cd client
ng add ngx-tailwind
```

Run Angular dev webserver via `ng serve -o`.

Add `Dockerfile`, `.dockerignore`, and `nginx.conf`.

Build prod app via Docker and run it:

```cmd
docker build -t agw-client .
docker run -it --rm -p 8080:80 agw-client
```

## Net6 WebAPI

Create via:

```cmd
mkdir backend
cd backend
dotnet new webapi
```

Disable HTTPS redirect and always enable Swagger (in `Program.cs`) and change applicationUrl to `http://localhost:5000` (in `Properties\launchSettings.json`).

Build via Docker and run it:

```cmd
docker build -t agw-backend .
docker run -it --rm -p 8080:80 agw-backend
```

## Docker Compose

Build all docker containers with `docker compose build`.

Startup all containers within a private network via `docker compose up` (press `Ctrl-C` to shutdown).

* Webapp: http://localhost:8088/
* WebApi via reverse proxy: http://localhost:8088/api/WeatherForecast

## Portainer

[Portainer](https://www.portainer.io/) is a web user interface to manage docker containers and container stacks.

* Used Portainer Version: **1.24.2**
* Portainer Stacks support the [Docker Compose file format](https://docs.docker.com/compose/compose-file/) **v2**.

A new Portainer "Stack" can be created based on the `docker-compose.yml` file in this git repo.

* In the Portainer UI navigate to "Stacks" and choose [+ Add stack].
* Provide a name and create a stack based on git repository with repository url:

  `https://github.com/ramdacxp/angular-nginx-webapi`

* After download and build (!) the container images should be available to be executed.  
  This even works on an Rasberry Pi, where everything is built for the ARM architecture.

## Links

NGINX:

* <https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/>
* <https://stackoverflow.com/questions/64647425/angular-with-nginx-and-docker-compose>

Compose:

* <https://medium.com/geekculture/docker-net-core-5-0-angular-11-nginx-and-postgres-on-the-google-cloud-platform-pt-1-363160e34439>

## License

[MIT License](LICENSE)
