# Address Bind

일반적으로 database를 설치하게되면 localhost에 설치하게 되는데, 이는 외부에서 접근이 불가능하다. 따라서 외부에서 접근이 가능하도록 설정을 해주어야 한다.
지금까지 확인해본 database는 mysql, postgresql, redis인데 각 database마다 설정 방법이 조금씩 다르다.

## MySQL

MySQL의 경우에는 `bind-address`를 설정해주면 된다. `bind-address`는 `The MySQL server listens on a single network socket for TCP/IP connections. This socket is bound to a single address, but it is possible for an address to map onto multiple network interfaces. The`bind-address`option specifies which interface the MySQL server should listen to. By default, the server listens to`localhost`which means it can only be accessed from the same machine. You can specify an IP address or a hostname to listen on. To specify multiple interfaces, use multiple`bind-address`options. To specify all interfaces, use`

## PostgreSQL

PostgreSQL의 경우에는 `listen_addresses`를 설정해주면 된다. `listen_addresses`는 `
Specifies the TCP/IP address(es) on which the server is to listen for connections from client applications. The value takes the form of a comma-separated list of host names and/or numeric IP addresses. The special entry \* corresponds to all available IP interfaces. The entry

## Redis

Redis의 경우에는 `bind`를 설정해주면 된다. `bind`는 `
By default, Redis listens for connections from all the network interfaces available on the server. It is possible to listen to just one or multiple selected interfaces using the bind directive followed by one or more IP addresses. For instance:
bind

## 참고

- [MySQL bind-address](https://dev.mysql.com/doc/refman/5.7/en/server-options.html#option_mysqld_bind-address)
- [PostgreSQL listen_addresses](https://www.postgresql.org/docs/9.1/runtime-config-connection.html)
- [Redis bind](https://redis.io/topics/security)
- [on-premise vs cloud](https://7942yongdae.tistory.com/82)
- [How to allow remote connections to MySQL?](https://stackoverflow.com/questions/15663001/how-to-allow-remote-connections-to-mysql)
- [How to allow remote connections to PostgreSQL?](https://stackoverflow.com/questions/839279/how-to-allow-remote-connections-to-postgresql-database)
- [How to allow remote connections to Redis?](https://stackoverflow.com/questions/19602529/redis-server-on-remote-server)
- [How to allow remote connections to MongoDB?](https://stackoverflow.com/questions/20796714/how-do-i-enable-remote-access-of-mongodb)
- [How to allow remote connections to Elasticsearch?](https://stackoverflow.com/questions/43614503/how-to-allow-remote-connections-to-elasticsearch)
- [How to allow remote connections to Neo4j?](https://stackoverflow.com/questions/43614503/how-to-allow-remote-connections-to-elasticsearch)
- [How to allow remote connections to RabbitMQ?](https://stackoverflow.com/questions/43614503/how-to-allow-remote-connections-to-elasticsearch)
- [How to allow remote connections to Kafka?](https://stackoverflow.com/questions/43614503/how-to-allow-remote-connections-to-elasticsearch)
- [How to allow remote connections to Zookeeper?](https://stackoverflow.com/questions/43614503/how-to-allow-remote-connections-to-elasticsearch)
- [How to allow remote connections to Cassandra?](https://stackoverflow.com/questions/43614503/how-to-allow-remote-connections-to-elasticsearch)
- [How to allow remote connections to HBase?](https://stackoverflow.com/questions/43614503/how-to-allow-remote-connections-to-elasticsearch)
- [How to allow remote connections to Hadoop?](https://stackoverflow.com/questions/43614503/how-to-allow-remote-connections-to-elasticsearch)
- [How to allow remote connections to Spark?](https://stackoverflow.com/questions/43614503/how-to-allow-remote-connections-to-elasticsearch)
- [How to allow remote connections to HDFS?](https://stackoverflow.com/questions/43614503/how-to-allow-remote-connections-to-elasticsearch)
- [How to allow remote connections to Hive?](https://stackoverflow.com/questions/43614503/how-to-allow-remote-connections-to-elasticsearch)
- [How to allow remote connections to HBase?](https://stackoverflow.com/questions/43614503/how-to-allow-remote-connections-to-elasticsearch)
