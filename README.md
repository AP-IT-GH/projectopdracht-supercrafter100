# Running services

- [Traefik](https://traefik.school.supercrafter100.com/) (https://traefik.school.supercrafter100.com/)
- [Zipkin](https://tracing.school.supercrafter100.com/) (https://tracing.school.supercrafter100.com/)
- [InfluxDB](https://metrics.school.supercrafter100.com/) (https://metrics.school.supercrafter100.com/)

Traefik: Reverse proxy
Zipkin: Used for tracing network requests
InfluxDB: Used for metrics on traefik

# How to deploy all services

1. First of all, all services in the traefik-addons directory should be deployed
    - **influxdb**: Deploy instructions can be found in the readme of it's folder
    - **zipkin**: run `docker compose up` inside it's directory to deploy it.
2. Deploy traefik itself by following the instructions provided in the readme in the traefik folder.
3. Deploy the example project provided in the project directory by following it's readme