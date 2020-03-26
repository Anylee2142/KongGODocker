
all: clean 

network-create:
	docker network create --driver bridge gogumball-net

network-inspect:
	docker network inspect gogumball-net

go-build:
	go build gumball

docker-build:
	docker build . -t gogumball

mysql-start-expose:
	docker run -d --name mysql --network gogumball-net -e MYSQL_ROOT_PASSWORD=12345 -p 3306:3306 mysql:5.5

mysql-start-internal:
	docker run -d --name mysql --network gogumball-net -e MYSQL_ROOT_PASSWORD=12345 mysql:5.5

mysql-shell:
	docker exec -it mysql bash

gumball-start-expose:
	docker run -d --name gogumball --network gogumball-net -p 3000:3000 gogumball

gumball-start-internal:
	docker run -d --name gogumball --network gogumball-net gogumball

gumball-shell:
	docker exec -it gogumball bash

cassandra-start-expose:
	docker run -d --name kong-database \
                   --network=gogumball-net \
                   -p 9042:9042 \
                   cassandra:3

cassandra-start-internal:
	docker run -d --name kong-database \
                   --network=gogumball-net \
                   cassandra:3

bootstrap:
	docker run --rm \
		--network=gogumball-net \
		-e "KONG_DATABASE=cassandra" \
 		-e "KONG_PG_HOST=kong-database" \
		-e "KONG_PG_PASSWORD=kong" \
		-e "KONG_CASSANDRA_CONTACT_POINTS=kong-database" \
		kong:2.0.2 kong migrations bootstrap

kong-start:
	docker run -d --name kong \
         --network=gogumball-net \
         -e "KONG_DATABASE=cassandra" \
         -e "KONG_PG_HOST=kong-database" \
         -e "KONG_PG_PASSWORD=kong" \
         -e "KONG_CASSANDRA_CONTACT_POINTS=kong-database" \
         -e "KONG_PROXY_ACCESS_LOG=/dev/stdout" \
         -e "KONG_ADMIN_ACCESS_LOG=/dev/stdout" \
         -e "KONG_PROXY_ERROR_LOG=/dev/stderr" \
         -e "KONG_ADMIN_ERROR_LOG=/dev/stderr" \
         -e "KONG_ADMIN_LISTEN=0.0.0.0:8001, 0.0.0.0:8444 ssl" \
         -p 8000:8000 \
         -p 8443:8443 \
         -p 8001:8001 \
         -p 8444:8444 \
         kong:2.0.2

install-curl:
	apt-get update; apt-get install curl
	yum install curl

remove: remove-network
	docker rm -f starbucks
	docker rm -f kong-database
	docker rm -f kong

sleep:
	sleep 40

remove-network:
	docker network rm gogumball-net

kong-setup: cassandra-run-expose sleep bootstrap kong-run