### 查看Kafka Connect

- 打开一个新终端并检查 Kafka Connect 服务的状态：

```sh
curl -H "Accept:application/json" localhost:8083/
```

- 检查向 Kafka Connect 注册的连接器列表：

```sh
curl -H "Accept:application/json" localhost:8083/connectors/
```

### 部署 MySQL 连接器

- 打开一个新终端，并使用curl命令注册 Debezium MySQL 连接器。

```sh
curl -i -X POST -H "Accept:application/json" -H "Content-Type:application/json" localhost:8083/connectors/ -d '{ "name": "inventory-connector", "config": { "connector.class": "io.debezium.connector.mysql.MySqlConnector", "tasks.max": "1", "database.hostname": "10.75.20.212", "database.port": "3309", "database.user": "root", "database.password": "debezium", "database.server.id": "184054", "database.server.name": "dbserver1", "database.include.list": "inventory", "database.history.kafka.bootstrap.servers": "dev-node1:9092,dev-node1=2:9092,dev-node3:9092", "database.history.kafka.topic": "rickdbhistory.inventory" } }'
```