1. gradle build
2. docker build -t portal-app .
3. docker run -p 9200:9200 -e "http.host=0.0.0.0" -e "transport.host=127.0.0.1" docker.elastic.co/elasticsearch/elasticsearch:6.3.0
4. docker run -p 8080:8080 --name portal-app-server --link mysql:salemysql --link nervous_carson:portalapp-es  portal-app
5. docker run -p 8080:8080 --name portal-app-server --link mysql:salemysql --link nervous_carson:portalapp-es  portal-app



## 批量删除容器
```
docker rm $(docker ps -a -q --filter "name=portal-app-com_app.")
```