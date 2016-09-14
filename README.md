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
5. Define the ports to avoid collisions with other applications, making
sure to map to the default port.
e.g.

    ```yml
    services:
      web:
        image: web
        environment:
          VIRTUAL_HOST: mysite.com
        ports:
          - "8080:80"
    ```

5. Define the following network your application's Docker Compose file 
(at the bottom of the file, outside of `services`):

    ```yml
    networks:
      front:
        external: true
    ```

6. Use the front network on the desired services by adding:
7.

    ```yml
    networks:
      - front
    ```

    e.g.

    ```yml
    services:
      web:
        image: web
        container_name: web
        networks:
          - front
    ```

7. Commit, push, and pull on your host (web) server.
8. Run `docker-compose up -d --build` or a custom build script.

### Setting Up Basic Authentication Support

To secure your virtual host, create a htpasswd file named as its equivalent `VIRTUAL_HOST` variable in `config/htpasswd`.

For example, if you have `VIRTUAL_HOST: more.cool.com`, create a htpasswd file at `config/htpasswd/more.cool.com`.

[How to Create an htpasswd file](http://httpd.apache.org/docs/2.2/programs/htpasswd.html)
