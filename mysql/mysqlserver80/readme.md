docker build -t mysqlserver80 .
docker run -e MYSQL_ROOT_PASSWORD=root -p 3380:3306 mysqlserver80