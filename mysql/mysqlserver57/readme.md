docker build -t mysqlserver57 .
docker run -e MYSQL_USER=root MYSQL_ROOT_PASSWORD=root -p 3357:3306 mysqlserver57