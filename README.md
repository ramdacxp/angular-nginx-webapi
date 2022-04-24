# Angular NGINX WebAPI setup for Docker Compose

This repo contains my reference `Dockerfile`s and config to

* Angular app
  * Build in Docker
  * Host via NGINX webserver in Docker Container
* WebAPI
  * Provided by DotNet 6 Kestrel webserver
  * Executed in Docker container
* Docker Compose
  * Build and hosting of all containers
  * WebAPI NGINX Reverse Proxy for container network
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

## Portainer

[Portainer](https://www.portainer.io/) is a web user interface to manage docker containers and container stacks.

* Used Portainer Version: **1.24.2**
* Portainer Stacks support the [Docker Compose file format](https://docs.docker.com/compose/compose-file/) **v2**.

## Links

NGINX:

* <https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/>
* <https://stackoverflow.com/questions/64647425/angular-with-nginx-and-docker-compose>

Compose:

* <https://medium.com/geekculture/docker-net-core-5-0-angular-11-nginx-and-postgres-on-the-google-cloud-platform-pt-1-363160e34439>

## License

[MIT License](LICENSE)
