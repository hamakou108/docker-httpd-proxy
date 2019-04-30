# docker-httpd-proxy

This is the repository to study Apache HTTP Server as forward/reverse proxy by use of Docker.

## Information

| certificate | passphrase of the private key | Common Name |
| :-- | :-- | :-- |
| root (CA) | my_ca_pass | my-ca |
| server | (decrypted) | my-server |
| client | (decrypted) | my-client |

## Usage

### Run Docker containers

```
$ git clone git@github:hamakou108/docker-httpd-proxy.git
$ cd docker-httpd-proxy
$ docker-compose up -d
```

### Update Apache configuration file

```
$ docker cp ./server/httpd.conf docker-httpd-proxy_server_1:/usr/local/apache2/conf/
$ docker cp ./server/httpd-ssl.conf docker-httpd-proxy_server_1:/usr/local/apache2/conf/extra/
$ docker-compose restart
```

### Send HTTP Requests to the web server from the client

```
$ docker exec -it docker-httpd-proxy_client_1 curl http://my-server
$ docker exec -it docker-httpd-proxy_client_1 curl http://my-server -x my-forward-proxy:8080
```

#### HTTPS with server/client certificates

```
$ docker exec -it docker-httpd-proxy_client_1 curl -k https://my-server --cert ./client.crt --key ./client.key
$ docker exec -it docker-httpd-proxy_client_1 curl -k https://my-server --cert ./client.crt --key ./client.key -x my-forward-proxy:8080
```

