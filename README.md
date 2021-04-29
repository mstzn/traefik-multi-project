# traefik-multi-project


## Configuration


- Set Traefik version (TRAEFIK_VERSION) on .env file in traefik folder 




1. `docker network create --driver=bridge --attachable --internal=false traefik_gateway`

2. `cd traefik`

3. `docker-compose up -d`

4. `cd ..`

5. `cd project1`

6. `docker-compose up -d`

7. continue step 4, 5, 6 for other project folders