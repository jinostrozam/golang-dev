#### DOCKER COMPOSE

Compilar docker compose cada vez que se edita el docker-compose.yaml
```
docker-compose build golang
```


Correr docker-compose en el background

```
docker-compose up -d
```

<br>


#### CONTAINER


Correr imagen docker en forma manual

```
docker run -it -v ${PWD}:/work -p 5001:5000 jinostroza/golang:1.0.0 sh

```


Conectarse a un container

```
docker exec -it [CONTAINER-ID] sh
```

Para conocer el id de un container ejecutar 
```
docker ps
```

#### DOCKER MULTISTAGE
```

// START STAGE 1 (DEV)

FROM base-SDK0-image-here   ---> LAYER 1

# Install dependencies
RUN go get ...              ---> LAYER 2

COPY source                 ---> LAYER 3

RUN build                   ---> LAYER 4

// END STAGE 1

// START STAGE 2 (PRODUCTION)

FROM runtime-image          ---> LAYER 5

COPY artifact-from-stage-1  ---> LAYER 6

RUN execute-aplication      ---> LAYER 7

// END STAGE 2

```

<br>

#### NOTAS

<br>

**Utilizando docker-compose**

Para crear un ambiente con docker-compose, se requiere indicar el ambiente Ej:

```
# Seleccionando container dev del multistage

build:
  target: dev
```

```
# Seleccionando container prod del multistage

build:
  target: prod
```

Para ejecutar prod, se requiere comentar los puntos montaje pues estan indicados en el dockerfile. Ej:

```
# working_dir: /work
# entrypoint: /bin/sh
# volumes:
# - ./golang/src/:/work
```

Levantando el multistage via docker-compose
```
docker-compose build
docker-compose up
```
<br>

**Sin docker-compose**

Crear la image docker del multistage completa

```
cd [carpeta con el docker file]
docker build . -t [nombre-del-container]
```

Luego ejecutar la imagen del multistage
```
docker run -d -p 5001:5000 [nombre-del-container]
```
<br>

Para crear una imagen de un stage especifico del multistage
```
cd [carpeta con el docker file]
docker build --target dev . -t [go-dev]
```

Para ejecutar stages distintos a prod, utilizar -it de lo contrario la imagen se ejecuta y cierra automaticamente
```
docker run -it -p 5001:5000 [go-dev] sh
```

<br>

Para acceder al container que se ejecuta en background (-d)
```
docker exec -it [CONTAINER-ID] sh
```
