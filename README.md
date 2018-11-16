# registry-testing

Repo for testing docker registry

## Self-Signed

Generate the self signed certs to run

Follow the official [guide](https://docs.docker.com/registry/insecure/#use-self-signed-certificates)

## Create authentications

Create the user to authenticate

Follow the official [guide](https://docs.docker.com/registry/deploying/#native-basic-auth)

## How to run with TLS + AUTH + different port

```docker run -d -p 5000:5000 --restart=always --name registry -v `pwd`/auth:/auth -e "REGISTRY_AUTH=htpasswd" -e "REGISTRY_AUTH_HTPASSWD_REALM=Registry Realm" -e REGISTRY_AUTH_HTPASSWD_PATH=/auth/htpasswd -v `pwd`/certs:/certs -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/domain.crt -e REGISTRY_HTTP_TLS_KEY=/certs/domain.key registry:2.6.2```

## How to run TLS in port 443 with Registry Mapping

```docker run -d -p 443:443 --restart=always --name registry -v `pwd`/auth:/auth -e "REGISTRY_AUTH=htpasswd" -e "REGISTRY_AUTH_HTPASSWD_REALM=Registry Realm" -e REGISTRY_AUTH_HTPASSWD_PATH=/auth/htpasswd -v `pwd`/certs:/certs -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/domain.crt -e REGISTRY_HTTP_TLS_KEY=/certs/domain.key -e REGISTRY_HTTP_ADDR=0.0.0.0:443 -v /registry:/var/lib/registry registry:2.6.2```

## How to run TLS NO AUTH with Registry Mapping

```docker run -d -p 443:443 --restart=always --name registry -v `pwd`/certs:/certs -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/domain.crt -e REGISTRY_HTTP_TLS_KEY=/certs/domain.key -e REGISTRY_HTTP_ADDR=0.0.0.0:443 -v /registry:/var/lib/registry registry:2.6.2```

## How to run TLS NO AUTH with Registry Mapping + READONLY

```docker run -d -p 443:443 --restart=always --name registry -v `pwd`/certs:/certs -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/domain.crt -e REGISTRY_HTTP_TLS_KEY=/certs/domain.key -e REGISTRY_HTTP_ADDR=0.0.0.0:443 -v /registry:/var/lib/registry -e REGISTRY_STORAGE_MAINTENANCE_READONLY='enabled: true' registry:2.6.2```

Documentation says that the Environment variable should be `REGISTRY_STORAGE_MAINTENANCE_READONLY_ENABLED=true`, but it fails every time you start the registry.
Found in a [PR][1] that the way to do it if you don't have any other maintenance value in the Environment variables is like this `REGISTRY_STORAGE_MAINTENANCE_READONLY='enabled: true'`

[1]: https://github.com/docker/distribution/pull/827#issuecomment-130097866

## Using docker-compose

`docker-compose up -d`

## Run using a custom config.file

```
docker run -d -p 5000:5000 --restart=always --name registry -v `pwd`/config.yml:/etc/docker/registry/config.yml registry:2.6.2
```


## Login

`docker login myregistrydomain.com:5000`


## Logout

`docker logout myregistrydomain.com:5000`
