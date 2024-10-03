# Nginx Basic Auth

A simple demo of using Nginx as a reverse proxy to add basic authentication.

it is a copy of https://gist.github.com/laurentbel/c4c7696890fc71c8061172a932eb52e4

just add env var `BIND_PORT`
added `FORWARD_PROTOCOL` to allow to redirect also https calls

## Example

```yaml
services:
  application:
    image: httpd
    networks:
      - mynetwork

  nginx:
    image: vikmstr/nginx-basic-auth
    ports:
      - "80:3000"
    depends_on:
      - application
    environment:
      - BIND_PORT=3000
      - FORWARD_HOST=application
      - FORWARD_PORT=80
      - FORWARD_PROTOCOL=http
      - BASIC_USERNAME=john.doe
      - BASIC_PASSWORD=myp@ssword!
    networks:
      - mynetwork

networks:
  mynetwork:
```

## Loki auth example
```yaml
services:
  nginx:
    image: vikmstr/nginx-basic-auth
    ports:
      - "80:3000"
    depends_on:
      - application
    environment:
      - BIND_PORT=3000
      - FORWARD_HOST=localhost
      - FORWARD_PORT=3100
      - FORWARD_PROTOCOL=http
      - BASIC_USERNAME=loki
      - BASIC_PASSWORD=loki

```

## References

- [Nginx reverse proxy with basic authentication](https://gist.github.com/laurentbel/c4c7696890fc71c8061172a932eb52e4)
