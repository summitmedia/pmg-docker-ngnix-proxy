# pmg-docker-ngnix-proxy

Default nginx-proxy container for mapping hostname to correct Docker application container.

## Use

1. On your host (web) server, clone 
[pmg-docker-ngnix-proxy](https://github.com/summitmedia/pmg-docker-ngnix-proxy)
into your web root.
2. Navigate into `pmg-docker-nginx-proxy`.
3. Run `docker network create front`.
3. Run `docker-compose up -d --build`.
4. Following the nginx-proxy 
[example docker-compose.yml](https://github.com/jwilder/nginx-proxy/blob/master/docker-compose.yml),
add the code to your application's Docker Compose file.
5. Define the following network:
```networks:
     front:
       external: true```
6. Use the front network on the desired services by adding to the bottom
of the file:
```networks:
        - front```
7. Commit, push, and pull on your host (web) server.
8. Run `docker-compose up -d --build` or a custom build script.
