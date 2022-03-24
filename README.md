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



