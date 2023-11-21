# Running services

- [Traefik](https://traefik.school.supercrafter100.com/) (https://traefik.school.supercrafter100.com/)
- [Todo Service](https://s140024.devops-ap.be/) (https://s140024.devops-ap.be/)
- [Zipkin](https://tracing.school.supercrafter100.com/) (https://tracing.school.supercrafter100.com/)
- [InfluxDB](https://metrics.school.supercrafter100.com/) (https://metrics.school.supercrafter100.com/)
- [Portainer](https://portainer.school.supercrafter100.com/) (https://portainer.school.supercrafter100.com/)
- [Uptime Kuma](https://uptime.school.supercrafter100.com/) (https://uptime.school.supercrafter100.com/)
- [Forgejo](https://git.school.supercrafter100.com/) (https://git.school.supercrafter100.com/)
- [Grafana](https://grafana.school.supercrafter100.com/) (https://grafana.school.supercrafter100.com/)

Traefik: Reverse proxy

Todo Service: Service that combines both a database, backend and frontend in a single compose file. Provided by AP Hogeschool

Zipkin: Used for tracing network requests

InfluxDB: Used for metrics on traefik

Portainer: Visualisation of running containers and managing them

Uptime Kuma: Uptime monitoring of the hosted services

Forgejo: Software forge with alternate github repository

Grafana: Visualisations of metrics of Traefik

# How to deploy all services

1. First of all, all services in the traefik-addons directory should be deployed
    - **influxdb**: Deploy instructions can be found in the readme of it's folder
    - **zipkin**: run `docker compose up` inside it's directory to deploy it.
2. Deploy traefik itself by following the instructions provided in the readme in the traefik folder.
3. Deploy the example project provided in the project directory by following it's readme

# TODO

- [x] https://docs.portainer.io/start/install-ce
- [ ] Jenkins
- [ ] Authentication on zipkin so it's not public to the internet (2 flies in 1 hit by using the central authentication?)
- [ ] Write documentation for deployment of all services
- [x] Grafana to visualize the data of InfluxDB (traefik)
- [x] Monitoring
- [ ] Central authentication (lookup traefik docs?) (https://github.com/travisghansen/external-auth-server, https://doc.traefik.io/traefik/middlewares/http/forwardauth/)
- [x] Software forge (forgejo)
