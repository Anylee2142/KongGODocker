## Kong 2.0.2 with cassandra
- https://docs.konghq.com/2.0.x/getting-started/introduction/
- https://medium.com/@vasista/explaining-kong-plugins-key-authentication-and-rate-limiting-on-flask-api-9f922c4f051

## Pre-requisite
Docker latest.    
Kong 2.0.2         
Cassandra 3.0       
Go 1.13.3         
MySQL 5.5      
     
    
## How to build
0. Go to gumball folder
1. make network-create
2. alias gopath='export GOPATH=$(pwd);export PATH=$PATH:$GOPATH/bin'
3. gopath
4. make go-build
	- db, err := sql.Open("mysql", "<username>:<pw>@tcp(<HOST>:<port>)/<dbname>")
5. make docker-build
6. make mysql-start
7. Go into mysql container and do `/mysql_execute.txt`
8. make gumball-start
9. make cassandra-start
10. make bootstrap
11. make kong-start


## Kong Steps
1. Add a Service
2. Add a Route
3. Add a Consumer
4. Add a Key-Auth to the Service
5. Set a API Key to the Consumer
6. Test APIs

## Test with postman collection and environement at root folder !
