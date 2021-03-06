# Installation des Galeraclusters auf Google

Es wurden drei maschinen jeweils mit Ubuntu und docker nach https://docs.docker.com/engine/installation/linux/ubuntulinux/

Dann werden die entsprechenden Maschinen gestartet:

#### Host 1

```bash
export HOST=10.0.0.2

docker run --detach \
  --name database01 \
  -e BOOTSTRAP=1 -e DEBUG=1 \
  -e MYSQL_PASS=password -e REP_PASS=replicate \
  -e HOST=$HOST -e SERVICE_DISCOVERY=env \
  -p $HOST:3306:3306 \
  -p $HOST:4444:4444 \
  -p $HOST:4567:4567 \
  -p $HOST:4568:4568 \
  paulczar/percona-galera
```
#### Host 2

```bash
export HOST=10.0.0.3
docker run --detach \
  --name database02 \
  -e BOOTSTRAP=1 -e DEBUG=1 \
  -e MYSQL_PASS=password -e REP_PASS=replicate \
  -e CLUSTER_MEMBERS=10.128.0.2 \
  -e HOST=$HOST -e SERVICE_DISCOVERY=env \
  -p $HOST:3306:3306 \
  -p $HOST:4444:4444 \
  -p $HOST:4567:4567 \
  -p $HOST:4568:4568 \
  paulczar/percona-galera
```

#### Host 3

```bash
export HOST=10.0.0.4
docker run --detach \
  --name database03 \
  -e BOOTSTRAP=1 -e DEBUG=1 \
  -e MYSQL_PASS=password -e REP_PASS=replicate \
  -e CLUSTER_MEMBERS=10.128.0.2 \
  -e HOST=$HOST -e SERVICE_DISCOVERY=env \
  -p $HOST:3306:3306 \
  -p $HOST:4444:4444 \
  -p $HOST:4567:4567 \
  -p $HOST:4568:4568 \
  paulczar/percona-galera

```


