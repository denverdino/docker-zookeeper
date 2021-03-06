docker-zookeeper
================

### Build

Builds a docker image for Zookeeper.

```docker build -t <user>/zookeeper:3.4.8 .```



### Play with Docker Compose

The ```docker-compose.yml``` is as following

```
version: "2"
services:
  zookeeper1:
      image: 'registry.aliyuncs.com/acs-sample/zookeeper:3.4.8'
      container_name: zookeeper1
      environment:
          - SERVER_ID=1
          - ADDITIONAL_ZOOKEEPER_1=server.1=0.0.0.0:2888:3888
          - ADDITIONAL_ZOOKEEPER_2=server.2=zookeeper2:2888:3888 
          - ADDITIONAL_ZOOKEEPER_3=server.3=zookeeper3:2888:3888
  zookeeper2:
      image: 'registry.aliyuncs.com/acs-sample/zookeeper:3.4.8'
      container_name: zookeeper2
      environment:
          - SERVER_ID=2
          - ADDITIONAL_ZOOKEEPER_1=server.1=zookeeper1:2888:3888
          - ADDITIONAL_ZOOKEEPER_2=server.2=0.0.0.0:2888:3888 
          - ADDITIONAL_ZOOKEEPER_3=server.3=zookeeper3:2888:3888
  zookeeper3:
      image: 'registry.aliyuncs.com/acs-sample/zookeeper:3.4.8'
      container_name: zookeeper3
      environment:
          - SERVER_ID=3
          - ADDITIONAL_ZOOKEEPER_1=server.1=zookeeper1:2888:3888
          - ADDITIONAL_ZOOKEEPER_2=server.2=zookeeper2:2888:3888 
          - ADDITIONAL_ZOOKEEPER_3=server.3=0.0.0.0:2888:3888
```


Deploy the Zookeeper Cluster with Docker Compose

```
docker-compose up -d
```

Check the status of zookeeper cluster

```
docker-compose log
```

