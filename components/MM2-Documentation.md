# mm2


## Crear topico Cluster Origen (A)
```
kafka-topics --create --topic prueba-mm2 --bootstrap-server <ORIGEN_BOOTSTRAP_SERVERS> --partitions 1 --replication-factor 1 --config retention.ms=9000000
## Cluster Origen
```
kafka-topics --create --topic prueba-mm2 --bootstrap-server <DESTINO_BOOTSTRAP_SERVERS> --partitions 1 --replication-factor 1 --config retention.ms=9000000```

## Cluster Destino (B)
```
kafka-console-consumer --bootstrap-server kafka2:9092 --topic test-topic --group test-group02
```


## Script para kafka

```
# describe topic

./kafka-topics --describe  --topic prueba-mm2 --bootstrap-server =b-1.othertest.uao6uu.c8.kafka.us-east-1.amazonaws.com:9092,b-2.othertest.uao6uu.c8.kafka.us-east-1.amazonaws.com:9092,b-3.othertest.uao6uu.c8.kafka.us-east-1.amazonaws.com:9092

Topic: prueba-mm2       PartitionCount: 1       ReplicationFactor: 1    Configs: min.insync.replicas=2,segment.bytes=1073741824,message.format.version=2.7-IV2,unclean.leader.election.enable=true
        Topic: prueba-mm2       Partition: 0    Leader: 2       Replicas: 2     Isr: 2  Offline:

# create topic
./kafka-topics --create  --topic prueba-mm2 --bootstrap-server b-1.othertest.uao6uu.c8.kafka.us-east-1.amazonaws.com:9092,b-2.othertest.uao6uu.c8.kafka.us-east-1.amazonaws.com:9092,b-3.othertest.uao6uu.c8.kafka.us-east-1.amazonaws.com:9092 --partitions 1 --replication-factor 1 --config min.insync.replicas=1 --config retention.ms=604800000



# create topic
./kafka-topics --create  --topic prueba-mm2 --bootstrap-server b-1.othertest.uao6uu.c8.kafka.us-east-1.amazonaws.com:9092,b-2.othertest.uao6uu.c8.kafka.us-east-1.amazonaws.com:9092,b-3.othertest.uao6uu.c8.kafka.us-east-1.amazonaws.com:9092 --partitions 1 --replication-factor 1 --config min.insync.replicas=1 --config retention.ms=604800000

```

## Topicos internos MM2

```sh
mm2-configs.msk.internal
mm2-offset-syncs.msk.internal
mm2-offsets.msk.internal
mm2-status.msk.internal

mm2-configs.apk.internal
mm2-offsets.apk.internal
mm2-status.apk.internal
apk.checkpoints.internal
apk.heartbeats

```

## Topicos internos del MirrorMaker2

```sh
# Origen
kafka-topics --create --topic mm2-configs.origen.internal --bootstrap-server <ORIGEN_BOOTSTRAP_SERVERS> --partitions 1 --replication-factor 1 --config cleanup.policy=compact --config retention.ms=9000000 --config min.insync.replicas=1

kafka-topics --create --topic mm2-offset-syncs.origen.internal --bootstrap-server <ORIGEN_BOOTSTRAP_SERVERS> --partitions 1 --replication-factor 1 --config cleanup.policy=compact --config retention.ms=9000000 --config min.insync.replicas=1

kafka-topics --create --topic mm2-status.origen.internal --bootstrap-server <ORIGEN_BOOTSTRAP_SERVERS> --partitions 1 --replication-factor 1 --config cleanup.policy=compact --config retention.ms=9000000 --config min.insync.replicas=1

kafka-topics --create --topic origen.checkpoints.internal --bootstrap-server <ORIGEN_BOOTSTRAP_SERVERS> --partitions 1 --replication-factor 1 --config cleanup.policy=compact --config retention.ms=9000000 --config min.insync.replicas=1

kafka-topics --create --topic origen.heartbeats --bootstrap-server <ORIGEN_BOOTSTRAP_SERVERS> --partitions 1 --replication-factor 1 --config cleanup.policy=compact --config retention.ms=9000000 --config min.insync.replicas=1


# destino
kafka-topics --create --topic mm2-configs.destino.internal --bootstrap-server <DESTINO_BOOTSTRAP_SERVERS> --partitions 1 --replication-factor 1 --config cleanup.policy=compact --config retention.ms=9000000 --config min.insync.replicas=1 

kafka-topics --create --topic mm2-offset-syncs.destino.internal --bootstrap-server <DESTINO_BOOTSTRAP_SERVERS> --partitions 1 --replication-factor 1 --config cleanup.policy=compact --config retention.ms=9000000 --config min.insync.replicas=1 

kafka-topics --create --topic mm2-status.destino.internal --bootstrap-server <DESTINO_BOOTSTRAP_SERVERS> --partitions 1 --replication-factor 1 --config cleanup.policy=compact --config retention.ms=9000000 --config min.insync.replicas=1 

kafka-topics --create --topic destino.checkpoints.internal --bootstrap-server <DESTINO_BOOTSTRAP_SERVERS> --partitions 1 --replication-factor 1 --config cleanup.policy=compact --config retention.ms=9000000 --config min.insync.replicas=1 

kafka-topics --create --topic destino.heartbeats --bootstrap-server <DESTINO_BOOTSTRAP_SERVERS> --partitions 1 --replication-factor 1 --config cleanup.policy=compact --config retention.ms=9000000 --config min.insync.replicas=1 


```


``` sh
kafka-producer-perf-test --topic prueba-mm2 --num-records 1000 --record-size 100 --throughput 1000 --producer-props bootstrap.servers=10.5.83.82:9092,10.5.83.81:9092

kafka-console-consumer --bootstrap-server 100.79.244.82:9092,100.79.244.81:9092  --topic apk.prueba-mm2

./kafka-topics --create  --topic apk.checkpoints.internal --bootstrap-server <b1:9092,b2:9092,b3:9092> --partitions 3 --config cleanup.policy=delete --replication-factor 1 --config min.insync.replicas=1 --config retention.ms=604800000

./kafka-topics --create  --topic apk.heartbeats --bootstrap-server <b1:9092,b2:9092,b3:9092> --partitions 3 --config cleanup.policy=delete --replication-factor 1 --config min.insync.replicas=1 --config retention.ms=604800000

```


## Crear conectores

Dentro del pod que tiene el mirrormaker, se usa el API REST del conector para modificar su configuracion

contector onpremise -> aws
```sh
curl -X POST -H "Content-Type: application/json" --data '{
  "name": "mm2-destino-a-origen",
  "config": {
    "connector.class": "org.apache.kafka.connect.mirror.MirrorSourceConnector",
    "clusters": "destino,origen",
    "source.cluster.alias": "destino",
    "target.cluster.alias": "origen",
    "source.cluster.bootstrap.servers": "<DESTINO_BOOTSTRAP_SERVERS>",
    "target.cluster.bootstrap.servers": "<ORIGEN_BOOTSTRAP_SERVERS>",
    "source.config.storage.replication.factor": "1",
    "target.config.storage.replication.factor": "1",
    "source.offset.storage.replication.factor": "1",
    "target.offset.storage.replication.factor": "1",
    "offset.syncs.topic.replication.factor": "1",
    "heartbeat.topic.replication.factor": "1",
    "checkpoint.topic.replication.factor": "1",
    "config.storage.replication.factor": "1",
    "status.storage.replication.factor": "1",
    "partitions": "1",
    "topics": "prueba.*",
    "tasks.max": "1",
    "replication.factor": 2,
    "refresh.topics.enabled": "true",
    "sync.topic.configs.enabled": "false",
    "emit.checkpoints.enabled": "true",
    "emit.heartbeats.enabled": "true",
    "checkpoints.topic": "mm2-offset-syncs.destino.internal",
    "heartbeats.topic": "mm2-heartbeats.destino.internal",
    "consumer.poll.timeout.ms": "500",
    "producer.linger.ms": "0",
    "consumer.client.id": "mm2-consumer",
    "producer.client.id": "mm2-producer"
  }
}' http://localhost:8083/connectors

```

## Para Conmutar los productores

1. Verificar el Offset del Clúster Origen

Utiliza el comando kafka-consumer-groups.sh para obtener información del grupo de consumidores en el clúster origen.

kafka-consumer-groups.sh --bootstrap-server <ORIGEN_BOOTSTRAP_SERVERS> --describe --group <GRUPO_CONSUMIDOR>


2. Verificar el Offset del Clúster Destino

Utiliza el mismo comando para verificar los offsets en el clúster destino:

kafka-consumer-groups.sh --bootstrap-server <DESTINO_BOOTSTRAP_SERVERS> --describe --group <GRUPO_CONSUMIDOR>


3. Comparar los Offsets del Clúster Origen y el Destino

El lag de replicación puede verificarse observando si el current-offset y el log-end-offset son iguales en ambos clústeres. Si son iguales, el lag es 0.
Ejemplo de Salida del Comando

GROUP           TOPIC           PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG
test-group      prueba-mm2      0          10000           10000           0

En este caso:

    Si LAG = 0, significa que no hay mensajes pendientes por replicar.
    Si el lag es mayor que cero, espera hasta que se sincronicen los offsets.




# ANEXOS

## Script kubernetes
```sh
kubectl get rolebindings,clusterrolebindings --all-namespaces
kubectl auth can-i '*' '*'
kubectl auth can-i create pods --all-namespaces
kubectl auth can-i list deployments.extensions
```
