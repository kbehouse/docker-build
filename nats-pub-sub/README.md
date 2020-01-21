
# nats-pub-sub in docker & k8s

## Build

```
docker build -t kbehouse/nats-pub-sub .
```

## Run in docker

```
#1 run docker in host
nats-server
#2 sub 
docker run --net=host kbehouse/nats-pub-sub sub -s localhost:4222 topicA
#3 pub 
docker run --net=host kbehouse/nats-pub-sub pub -s localhost:4222 topicA abcdefg
```

## Run in K8s/K3s

```
kubectl run  nats-pub-sub --image=kbehouse/nats-pub-sub -i --tty
```

```
# get pods name
kubectl get pods
kubectl exec -it [pod-name] bash
# pub or sub
sub -s [nats-server] [topic-name] 
```

