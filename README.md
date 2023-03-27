"main" 

CREATE CUSTOM BRIDGE NETWORK
docker network create db

START MYSQL SERVER WITH CUSTOM ROOT PASSWORD
docker run \
    --network db \
    -e MYSQL_ROOT_PASSWORD=my-secret-password \
    --name db \
    -d db

START PHPMYADMIN WITH PMA_HOST VARIABLE (over DNS name - name of the container)
docker run \
    --network db \
    -p 8080:80 \
    -e PMA_HOST=db \
    -d phpmyadmin/phpmyadmin
