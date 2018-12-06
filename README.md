# Turtl server in docker with Traefik

This is the new Turtl server under docker container with enabled Traefik as a reverse proxy

## Running the server

```sh
git clone git@github.com:moookino/docker-turtl-server.git
mv docker-turtl-server turtl
cd turtl
git clone https://github.com/turtl/server
cd server/
# create the plugin directory from config.yaml#plugins.plugin_location
mv example-plugins plugins/ #to avoid building errors if you don't want to use plugins
```

Now edit `config/config.yaml.default` as needed, but don't forget to change this parts:

```
db:
  connstr: 'postgres://slappy:floppy@postgres:5432/turtl'
  pool: 24

loglevel: 'debug'

app:
  enable_bookmarker_proxy: false
  api_url: 'http://t.example.com:8181'
  www_url: 'https://turtl.example.com'
```

Change db setting to `@postgres` or with name same as in docker-compose
Don't forget to change `api_url` and `www_url`

Now do:

```sh
sudo docker build -t turtl .
cd ..\
sudo docker-compose up -d
```