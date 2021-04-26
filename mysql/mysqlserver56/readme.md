docker build -t mysqlserver56 .
docker run -e MYSQL_ROOT_PASSWORD=root -p 3356:3306 mysqlserver56
 docker run --rm -it --entrypoint /bin/bash phpserver52