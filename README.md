# docker-httpd-proxy

This is the repository to study Apache HTTP Server as forward/reverse proxy by use of Docker.

## Information

| certificate | passphrase of the private key | Common Name |
| :-- | :-- | :-- |
| root (CA) | my_ca_pass | my-ca |
| server | my_server_pass (decrypted) | my-server |
| client | my_client_pass (decrypted) | my-client |
| reverse-proxy | my_reverse_proxy_pass (decrypted) | my-reverse-proxy |

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
$ docker exec -it docker-httpd-proxy_client_1 curl http://my-reverse-proxy/proxy
```

#### HTTPS with server/client certificates

```
$ docker exec -it docker-httpd-proxy_client_1 curl https://my-server --cert ./ssl/client-cert-dec.pem --key ./ssl/client-key-dec.pem --cacert ./ssl/cacert.pem
$ docker exec -it docker-httpd-proxy_client_1 curl https://my-server --cert ./ssl/client-cert-dec.pem --key ./ssl/client-key-dec.pem --cacert ./ssl/cacert.pem -x my-forward-proxy:8080
$ docker exec -it docker-httpd-proxy_client_1 curl https://my-reverse-proxy/proxy --cert ./ssl/client-cert-dec.pem --key ./ssl/client-key-dec.pem --cacert ./ssl/cacert.pem
```

