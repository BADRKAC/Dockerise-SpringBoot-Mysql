# How to run
```
git clone https://git-codecommit.eu-west-1.amazonaws.com/v1/repos/poc_docker_dev2prod
cd poc_docker_dev2prod
mvn clean package
docker pull mysql:5.6
docker run --name mysql-standalone -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=test -e MYSQL_USER=sa -e MYSQL_PASSWORD=password -d mysql:5.6
docker build . -t users-mysql
docker run -p 8084:8084 --name users-mysql --link mysql-standalone:mysql -d users-mysql
docker logs --follow users-mysql
```

# Test in browser
Get your ip {{your IP Machine}} using
```
docker-machine ip
```
and test 
Url : http://{{your IP Machine}}:8084/all/stagiaires

Result :
```
[{"id":1,"name":"BADR","salary":3400,"teamName":"GRP"}]
```

# Description

1- MVN package
```
mvn clean package
```
2- Utiliser l'image MySQL-5.6 publiée par Docker Hub  et sa configuration :

```
docker pull mysq
docker run --name mysql-standalone -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=test -e MYSQL_USER=sa -e MYSQL_PASSWORD=password -d mysql:5.6
```
3- build spring image with Dockerfile 
```
docker build . -t users-mysql
```

4- Run
```
docker run -p 8084:8084 --name users-mysql --link mysql-standalone:mysql -d users-mysql
```

5- Logs
```
docker logs --follow users-mysql
```

# How to remove containers
Les deux containers : users-mysql et mysql-standalone
```
docker stop users-mysql mysql-standalone
docker rm users-mysql mysql-standalone
```
