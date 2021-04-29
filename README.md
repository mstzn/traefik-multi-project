# traefik-multi-project

Did you get tired to setup your environment over and over again for every each project?

Clone this repository, make the necessary changes and done!

This repository allows you run multiple `PHP` projects locally and managed by `Traefik`.

The folder structure is designed to easily add more independent project folders.

---

**WARNING**

**Remember this repository is meant for development purposes, not production**


---

## Basic Setup

 ### SSL Certificates

- With following steps you can use SSL locally with generating certificates by `mkcerts`, if SSL is not necessary for you, simply rename `traefik-wo-ssl.toml` file to `traefik.toml`

- For generating SSL certificates to use "locally", you can use `mkcerts` -> https://github.com/FiloSottile/mkcert

- After generating certificates, place them under `traefik/certs` folder.


### 1. Shared Network Setup
```sh
docker network create --driver=bridge --attachable --internal=false traefik_gateway
```

### 2. Traefik Setup

```sh
cd traefik
```

```sh
docker-compose up -d
```

### 3. Project Setup

```sh
cd project1
```

```
docker-compose up -d
```

---
## Configuration / Explanation



### 1. Shared Network Setup

```sh
docker network create --driver=bridge --attachable --internal=false traefik_gateway
```

### 2. Traefik Setup

Set/Change Traefik version (TRAEFIK_VERSION) on .env file in traefik folder than follow steps below

```sh
cd traefik
```

```sh
docker-compose up -d
```

Once the installation complete, you can access traefik dashboard with `http://127.0.0.1:8080/dashboard/`


### 3. Project Setup

- This repository includes 3 project folders that you can use directly with `project1.domain.com`, `project3.domain.com`, `project3.domain.com`

- To change domain name: search for `domain.com` in whole project and replace it with your domain name.

- **NOTE**: For domain resolution, you have to make changes on your hosts file. You can find many ways to do this with a little search `how to change the hosts file on Linux` or `how to change the hosts file on Windows 10`

```sh
127.0.0.1   project1.domain.com
127.0.0.1   project2.domain.com
127.0.0.1   project3.domain.com
```

- To change `project1` to your project name, simply make a search with `project1` and replace it.

- Every each project includes following components/services/containers:

    - nginx
    - php-fpm
    - mariadb
    - redis
    - elasticsearch
    - composer

- Project folders also contain a .env file that you can change versions of services, DB credentials etc.

- To run your project follow the steps below:

```sh
cd project1
```

```
docker-compose up -d
```

repeat the steps for every each project folders