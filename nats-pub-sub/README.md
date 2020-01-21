
# nats-pub-sub in docker & k8s

## Run in docker

```
#1 run docker in host
nats-server
#2 sub 
docker run --net=host kbehouse/nats-pub-sub sub -s localhost:4222 topicA
#3 pub 
docker run --net=host kbehouse/nats-pub-sub pub -s localhost:4222 topicA abcdefg
```



