# registry-testing

Repo for testing docker registry

## Self-Signed

Generate the self signed certs to run

Follow the official [guide](https://docs.docker.com/registry/insecure/#use-self-signed-certificates)

## Create authentications

Create the user to authenticate

Follow the official [guide](https://docs.docker.com/registry/deploying/#native-basic-auth)

## How to run

```docker run -d -p 5000:5000 --restart=always --name registry -v `pwd`/auth:/auth -e "REGISTRY_AUTH=htpasswd" -e "REGISTRY_AUTH_HTPASSWD_REALM=Registry Realm" -e REGISTRY_AUTH_HTPASSWD_PATH=/auth/htpasswd -v `pwd`/certs:/certs -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/domain.crt -e REGISTRY_HTTP_TLS_KEY=/certs/domain.key registry:2.6.2```

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
