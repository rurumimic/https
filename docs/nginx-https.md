# Simple nginx HTTPS server

- nginx: [Configuring HTTPS servers](http://nginx.org/en/docs/http/configuring_https_servers.html)
- docker: [nginx](https://hub.docker.com/_/nginx)

---

## Test nginx HTTP server

Default Configurations:

- [/etc/nginx/nginx.conf](/nginx/default/nginx.conf)
- [/etc/nginx/conf.d/default.conf](/nginx/default/default.conf)

Run:

```bash
docker run --rm --name http-nginx -p 80:80 -d nginx:alpine
```

Go to [http://localhost](http://localhost)

Stop:

```bash
docker stop http-nginx
```

---

## Self signed certificate

Read [Self-signed Certificate](docs/../self-signed-certificate.md).

- RootCA Cert: [rootca.pem](/certs/self-signed/rootca.pem)
- RootCA Key: [rootca.key.pem](/certs/self-signed/rootca.key.pem)
- Cert: [cert.pem](/certs/self-signed/example.localhost/cert.pem)
- Key: [key.pem](/certs/self-signed/example.localhost/key.pem)
- Chained Cert: [example.localhost.chained.pem](/certs/self-signed/example.localhost.chained.pem)

---

## Configuration

- [/etc/nginx/nginx.conf](/nginx/https/nginx.conf)
- [/etc/nginx/conf.d/default.conf](/nginx/https/default.conf)

---

## Test nginx HTTPS server

Run in the project directory:

```bash
docker run --rm \
--name https-nginx \
-p 443:443 \
--hostname example.localhost \
-v $PWD/certs/self-signed:/etc/nginx/certs \
-v $PWD/nginx/https/nginx.conf:/etc/nginx/nginx.conf \
-v $PWD/nginx/https/default.conf:/etc/nginx/templates/default.conf.template \
-d nginx:alpine
```

Open [https://example.localhost](https://example.localhost)

Stop:

```bash
docker stop https-nginx
```

### Log

```log
172.17.0.1 - - [24/Jun/2020:12:49:14 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.106 Safari/537.36" "-"
172.17.0.1 - - [24/Jun/2020:12:49:43 +0000] "GET / HTTP/1.1" 200 396 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.1.1 Safari/605.1.15" "-"
```

---

## Clean up

### Keychain Access

1. Open Keychain Access
2. Remove `rootca.pem`, `cert.pem`

### `/etc/hosts`

Remove `127.0.0.1 example.localhost`
