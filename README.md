# NestedChain
# Read me

The project is the implementation of the nested blockchain system which consists of 1 main chain with 3 peer nodes and 3 sub chains with 2,2,3 peer nodes respectively. The network is a muti-machine deployment with 3 ali-cloud ECSs.



### Requirements:

1.docker

2.docker-compose

3.fabric(including faric samples, faric-ca, fabric binaries and images)

4.fabric-gateway

5.go



### Process

Step1: Start the host

Docker-swarm configuration of the following ports :

\1. 2377 (TCP) — 
\2. 7946 (TCP and UDP) — 
\3. 4789 (TCP and UDP) — 



Step2: Construct the overlay network

```
ssh -i <key> ubuntu@<public IP>

//Add other hosts to this cluster as managers
docker swarm init --advertise-addr <pc-1 ip address>docker swarm join-token manager
docker network create --attachable --driver overlay basic-network docker network ls
```



Step3: Set up identifications

```
./create-artifacts.sh
```

Copy the entire directory 'crypto config'  to other hosts



Step4: Start the docker compose

```
# from PC -1,
docker-compose -f pc1.yaml up -d#
docker-compose -f pc2.yaml up -d#
docker-compose -f pc3.yaml up -d#
```

To start the peer nodes and order nodes 



Step5: Create channel

```
./createChannel.sh
```

Init the channel and add nodes into corresponding channel.



Step6: Install chaincode

```
./deployChaincode.sh
```

The chaincode(smart contract ) is then installed on each peer node for transaction.


