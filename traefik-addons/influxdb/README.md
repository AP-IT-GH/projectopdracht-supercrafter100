# Issues encountered during installation on my end

Traefik still uses an older version of influxdb so the default udp method did not work, I had to switch over to the http method and then configure influx with it's v1 endpoints as it does not support the v2 endpoints yet. Which is why the setup is a bit of a hassle.

# Steps to deploy
1. Create a `.env` file and copy over the variables from the `.example.env` and fill them in
2. Start up the docker container
3. Open a shell in the container
4. Create a new config using:
```bash
$ influx config create \
  -n CONFIG_NAME \
  -u http://localhost:8086 \
  -p USERNAME:PASSWORD \
  -o ORG
```
replacing CONFIG_NAME with the name of the configuration, USERNAME with the admin username you made for your account, PASSWORD with the password you configured for the account and lastly ORG with the organization you chose.
5. Create a new bucket for traefik to use
```bash
$ influx bucket create -n traefik -o ORG -r 2h
```
replacing ORG with the organisation of the admin account
6. Now list the available buckets for your org so we can get the id using:
```bash
$ influx bucket ls -o ORG
```
replacing ORG with the organisation of the admin account. Copy the id of our newly created traefik bucket.
7. Create a new v1 authentication token for traefik to use using the following command:
```bash
$ influx v1 auth create --username traefik --password o1K55zydh5Vl --read-bucket BUCKET_ID --write-bucket BUCKET_ID
```
replacing BUCKET_ID with the id of the traefik bucket from the step earlier. If you end up changing the password here, you'll have to update this in the treafik.yml file of the traefik container.

# Accessing the web ui
The web of influxdb ui will be available on the domain configured in the traefik label of the compose file. 