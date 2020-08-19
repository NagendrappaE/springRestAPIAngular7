# springRestAPIAngular7 with  KONG API GATEWAY 



docker run -p 1337:1337 -e "TOKEN_SECRET={{somerandomstring}}" -e "DB_ADAPTER=postgres" -e "DB_HOST=localhost" -e "DB_PORT=5432"  -e "DB_USER=postgres" -e "DB_PASSWORD=root"             -e "DB_DATABASE=postgres"            -e "NODE_ENV=development"          --name konga         pantsel/konga


https://tech.david-cheong.com/managing-microservices-and-apis-with-kong-and-konga/

$ docker network create kong-net


docker run -d --name kong-database --network=kong-net -p 5432:5432 -e “POSTGRES_USER=kong” -e “POSTGRES_DB=kong” postgres:9.6


docker run --rm --network=kong-net -e "KONG_DATABASE=postgres" -e "KONG_PG_HOST=kong-database" kong:latest kong migrations up




docker run -d --name kong --network=kong-net -e "KONG_DATABASE=postgres" -e "KONG_PG_HOST=kong-database" -e "KONG_PROXY_ACCESS_LOG=/dev/stdout" -e "KONG_ADMIN_ACCESS_LOG=/dev/stdout" -e "KONG_PROXY_ERROR_LOG=/dev/stderr" -e "KONG_ADMIN_ERROR_LOG=/dev/stderr" -e "KONG_ADMIN_LISTEN=0.0.0.0:8001, 0.0.0.0:8444 ssl" -p 8000:8000 -p 8443:8443 -p 8001:8001 -p 8444:8444 kong:latest








#######################################use the below link for kong service and router configuration##############

https://docs.konghq.com/0.13.x/getting-started/configuring-a-service/


###service

curl -i -X POST \
  --url http://localhost:8001/services/ \
  --data 'name=example-service' \
  --data 'url=http://jboss.evolvus.io/esign/'

#router

curl -i -X POST \
  --url http://localhost:8001/services/emandate-servicce/routes \
  --data 'hosts[]=jboss.evolvus.io'



###checking the response  accessing the application 



http://jboss.evolvus.io:8000/add



curl -i -X GET \
  --url http://localhost:8000/add \
  --header 'Host: jboss.evolvus.io'



############for proxy configuration############


https://docs.konghq.com/1.4.x/proxy/


