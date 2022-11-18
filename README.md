# parex

[![Releases](https://img.shields.io/badge/version-1.0.1-orange)](#)
[![Jenkins Build](https://img.shields.io/badge/build-passing-brightgreen)](#)
[![Docker Build](https://img.shields.io/badge/docker%20build-passing-brightgreen)](#)
[![Docker Image](https://img.shields.io/docker/image-size/parex/parex/latest?color=green)](#)
[![Docker Pulls](https://img.shields.io/docker/pulls/parex/parex?color=red)](https://hub.docker.com/repository/docker/parex/parex)
[![LICENSE](https://img.shields.io/badge/license-Apache-lightgray)](https://github.com/parex/parex/blob/master/LICENSE)

parex is the newest technology for `blockchain` and can be used as a payment gateway.

- [`parex`](https://parexscan.io) : The official web page of parex


This guide is used by dozens of product teams at parex. Have a question or comment? [Open an issue!](https://github.com/parex/parex/issues/new)

- [Release Notes](#public-release-notes)
- [parex Node Requirements](#wrench-system-requirements)
- [Pre-Installation Steps](#package-pre-installation-steps)
- [Usage](#computer-usage)
- [FAQ](#books-faq)
- [Roadmap](#roadmap)



## Public Release Notes

##### v2.5.0
- Parex Network 


##### v2.4.5d
- Various improvements for fast sync 


##### v2.4.5c
- 3.0 integration bugs


##### v2.4.5a
- Burn Approve List
- "http://{DockerHostIP}:2020/getBurnApproveList/" 
  - result : hash

- Burn Approve
- "http://{DockerHostIP}:2020/setBurnApprove/{hash}" 


##### v2.4.5
- TestChain bugs
- infrastructure development for AVAXBridge


##### v2.4.4a
- "http://{DockerHostIP}:2020/getMasterPackage/" 



##### v2.4.4
- "http://{DockerHostIP}:2020/setChangeMasterPackage/{masterpackagehash}" 


##### v2.4.3c
- "http://{DockerHostIP}:2020/setCompleteInsurancePay/" 


##### v2.4.3b
- "http://{DockerHostIP}:2020/setPRXUIDCode/{PRXUIDCODE}" 
- "http://{DockerHostIP}:2020/getPRXUIDCode/" 


##### v2.4.3a
- "http://{DockerHostIP}:2020/setChangeClouder/{CommunityCode}" 
- must be have same Percent and same DexTrackerNo

##### v2.4.3
- "http://{DockerHostIP}:2020/setNewMasterPackage/" 
- must be have  (5000 PRX) on Pool Main Wallet

##### v2.4.2
- "http://{DockerHostIP}:2020/getPoolWallet/" 
- Pool Main Wallet for Insurance


##### v2.4.1
- "http://{DockerHostIP}:2020/setChangePool/{poolApiKey}"


##### v2.4.0
- Improve transaction indexing performance
- The SyncProgress method fixed bugs
- 3.0 bridge testing
- the engine APIs testnet transaction signing
- performance improvements
- testnet 3.0 bridge have been modernized 


##### v2.3.8
- Case Sensitive DexHash scan
##### v2.3.7
- PRX Mining With ParexPackage(CloudPartner)
- fix CloudPartner CommunityCode
##### v2.3.6
- PRX Mining With ParexPackage(CloudTracker)
##### v2.3.5
- getFee
- getmyWallet
##### v2.3.4
- setCloudTracker
##### v2.3.3
- sync optimization
##### v2.3.2
- setMasterPackage
- Maximum Pool Member Limit Canceled
##### v2.3.1
- optimize sync
##### v2.3.0
- parex Node Offline Sync (Fastest Way) https://backup.parex.io
##### v2.2.10
- online status optimized
##### v2.2.9
- fast syncing 
##### v2.2.8
- getParexKey 
##### v2.2.7
- IP Restrict and MAC Restrict (1 pc 1 DexTracker) or (1 pc 1 MasterTracker)
- Mining will start after synchronization is complete 
- Maximum Pool Member Limit (DexTracker) : 200
##### v2.2.6
- masterTracker optimization
##### v2.2.5
- sendtransaction optimization
##### v2.2.4
- "http://{DockerHostIP}:2020/setPoolServiceFee/{percent}” 
##### v2.2.3
- DXC Mining
- Dual Coin Mining (PRX)
##### v2.2.2
- Adding DRSProtocol (Duplicate Record Security Protocol)
- Locks same transaction one minute per node

##### v2.2.1
- Added Master Tracked (Now DeFi Supported)
- Docker Socket Extention fixed

##### v1.0.1
- Fixed PostgreSQL PID Lock Problem
- Fixed Block Logs 

## :wrench: System Requirements
### DexTracker
- parex Node Minimum Requirements: **`2 Core`** of CPU **`8GB`** of Memory and **`3TB`** of SSD
- Tested Operation Systems `Windows Server 2016 or Later` || `Centos` || `Ubuntu` || `Amazon Linux`
- At Least `5mbit` of `Internet Connection` with Port `2020` Ingress from **Your IP** Allowed

### MasterTracker
- parex Node Minimum Requirements: **`8 Core`** of CPU **`16GB`** of Memory and **`3TB`** of SSD
- Tested Operation Systems `Windows Server 2016 or Later` || `Centos` || `Ubuntu` || `Amazon Linux`
- At Least `20mbit` of `Internet Connection` with Port `2053` Ingress from **Your IP** Allowed


## :package: Pre-Installation Steps

:warning: parex is fully docker compatible and please follow [Windows](https://docs.docker.com/docker-for-windows/install/), [Centos](https://docs.docker.com/engine/install/centos/), [Ubuntu](https://docs.docker.com/engine/install/ubuntu/), [Amazon Linux](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/docker-basics.html), [MAC OS](https://docs.docker.com/docker-for-mac/install/) installation steps before running parex Node. After docker installation open a command line || terminal and run command to check the docker version.

```
docker -v
```

> **Output**: Docker version 20.10.0, build 7287ab3



### parex Node Offline Sync (Fastest Way)
To catchup block syncs we publish blocks in zipped format. You can download block archives and catchup quickly. This way is usefull for clean node deployements .

[`Quick sync is only possible on initial setup. Do not use this way for current nodes.`]


Steps: 
 - Start the node to trigger initial Database Schemas.
 - Download the archive.
 - Unzip files to docker volume.
 - Start the node 

Offline Blocks Link: https://backup.parex.io

Commands to Execute:
```
wget https://backup.parex.io/data-[date].tar.gz
```
Stop parex node
```
docker kill parex
```
Delete old data dir
```
rm -rf /var/lib/docker/volumes/parex/_data/12
```
Untar archive to data dir
```
tar -zxvf data-[date].tar.gz -C /var/lib/docker/volumes/parex/_data/
```
And start the node
```
docker run -d --rm -p 2020:2020 -p 2053:3030 -v parex:/var/lib/postgresql/ --privileged --log-driver=none --name parex parex/parex:latest
```

## :computer: Usage

##### 1. Run parex:

parex docker file is stored in dockerhub and ready for use with command: (Please check the version and use as tag rather than latest)

```
docker run -d --rm -p 2020:2020 -p 2053:3030 -v parex:/var/lib/postgresql/ --privileged --log-driver=none --name parex parex/parex:latest
```

After docker container **comes up** run the command;

```
docker ps
```

> **Output**: db641c6c55b7   parex/parex   "/startup.sh"   32 seconds ago   Up 31 seconds   0.0.0.0:2020->2020/tcp, 5432/tcp   parex


##### 2. Follow Blocks:

```
docker attach parex
```

##### 3. Node RestAPI commands :


```
"http://{DockerHostIP}:2020/getPoolWallet/”
```
- `value : Pool Main Wallet for Insurance` 

```
"http://{DockerHostIP}:2020/setCloudTracker/{communitycode}”
```
- `communitycode : CloudTracker Key(communitycode)` 

```
"http://{DockerHostIP}:2020/setStartDXCMiner/”
```

```
"http://{DockerHostIP}:2020/setStartPRXMiner/”
```

```
"http://{DockerHostIP}:2020/getTrackerKey/”
```
- `trackerkey : TrackerKey for Purchase DexLife` 

```
"http://{DockerHostIP}:2020/setMasterPackage/{dexhash}”
```
- `dexhash : DexChain Transaction Hash` 

```
"http://{DockerHostIP}:2020/getParexKey/”
```
- `parexkey : ParexKey for Purchase Parex Package` 

```
"http://{DockerHostIP}:2020/setMasterTracker/{pool}&{hostname}&{percent}”
```
- `pool : MasterTracker Pool Name` 
- `hostname : MasterTracker Host Name`
- `percent : MasterTracker Pool Cost Percent % range (%5-%50)`

```
"http://{DockerHostIP}:2020/setPoolServiceFee/{percent}”
```
- `percent : MasterTracker Pool Cost Percent % range (%5-%50)`

```
"http://{DockerHostIP}:2020/setJoinPool/{poolapikey}”
```
- `poolapikey : MasterTracker PoolApiKey` 

"http://{DockerHostIP}:2020/setNickname/{nickName}”
```
- `nickName : DexChain Tracker Nickname` 
```
“http://{DockerHostIP}:2020/isWallet/{address}”
```
- `address: Dexchain Address`
```
"http://{DockerHostIP}:2020/balanceWallet/{address}"
```
- `address: Dexchain Address`
```
"http://{DockerHostIP}:2020/balanceToken/{address}&{contract}"
```
- `address: Dexchain Address`
- `contract: DexChain Contract Address (if null please set “parex”)`
```
“http://{DockerHostIP}:2020/createWallet/{password}”
```
- `password: Dexchain Address password “Please Don’t Forget it”`
```
"http://{DockerHostIP}:2020/getLastBlock/"
```
- `Last Block`
```
"http://{DockerHostIP}:2020/getTransactionByDexHash/{dexhash}"
```
- `dexhash: Dexchain Transaction Hash`
```
"http://{DockerHostIP}:2020/getTransactions/{address}&{limit}&{orderby}”
```
- `address: Dexchain Address`
- `limit: number of records`
- `orderby: ASC or DESC `
```
"http://{DockerHostIP}:2020/getTransactionByBlock/{blockid}&{limit}&{orderby}”
```
- `blockid: Block ID (hex)`
- `limit: number of records`
- `orderby: ASC or DESC `
```
"http://{DockerHostIP}:2020/getTransactionByBlockOffset/{blockid}&{limit}&{orderby}&{offset}”
```
- `blockid: Block ID (hex)`
- `limit: number of records`
- `orderby: ASC or DESC `
- `offset: skip that many rows before beginning to return rows `
```
"http://{DockerHostIP}:2020/getmyTransactionByBlock/{blockid}&{limit}&{orderby}”
```
- `blockid: Block ID (hex)`
- `limit: number of records`
- `orderby: ASC or DESC `
```
"http://{DockerHostIP}:2020/sendTransaction/{sender}&{password}&{receiver}&{amount}&{fee}&{contract}&{description}"
```
- `sender : Sender Dexchain Address`
- `password: Dexchain Address password`
- `receiver: Receiver Dexchain Address`
- `amount: Amount of DXC`
- `fee: Fee of Transaction (IN / OUT)` 
- `contract: DexChain Contract Address (if null please set “parex”)`
- `description: Statements of Transaction (if null please set “null”)`
```
"http://{DockerHostIP}:2020/getSendToken/”
```
- `Token: Unique Token GUID`
```
"http://{DockerHostIP}:2020/sendTransactionV2/{sendtoken}&{sender}&{password}&{receiver}&{amount}&{fee}&{contract}&{description}"
```
- `sendtoken : Unique Token GUID`
- `sender : Sender Dexchain Address`
- `password: Dexchain Address password`
- `receiver: Receiver Dexchain Address`
- `amount: Amount of DXC`
- `fee: Fee of Transaction (IN / OUT)` 
- `contract: DexChain Contract Address (if null please set “parex”)`
- `description: Statements of Transaction (if null please set “null”)`
```
"http://{DockerHostIP}:2020/getFee/{amount}&{contract}"
```
- `fee: Fee DXC`
```
"http://{DockerHostIP}:2020/getmyWallet/"
```
- `address: Dexchain Address`
- ```

"http://{DockerHostIP}:2020/setChangePool/{poolApiKey}"
```
- `poolApiKey: new poolApiKey`


## :books: FAQ

### How Can I Calc Fee
Sample Fee Calculation


| Transaction Amount | Fee %         | Fee Amount |
| :----------------: | :-----------: |:---------: |
|               1000 |         0.003 |     3.00   |
|              10000 |        0.0003 |    +2.70   |
|             100000 |       0.00003 |    +2.70   |
|            1000000 |      0.000003 |    +2.70   |
|           10000000 |     0.0000003 |    +2.70   |
|          100000000 |    0.00000003 |    +2.70   |
|         1000000000 |   0.000000003 |    +2.70   |
|        10000000000 |  0.0000000003 |    +2.70   |
|       100000000000 | 0.00000000003 |    +2.70   |
|                    |               |            |
|                    |               |    24.60   |


25000 parex Transaction = (1000 x 0.003) + (9000 x 0.0003) + (15000 x 0.00003) = 6.150 Fee

### Standard fee distribution
- %0,1 MasterTracker Bonus
- %0,1 DexClouder Bonus
- %0,1 DexConfirmer Bonus

### Commercial fee distribution
- %0,1 DexClouder ProActivist Bonus
- %0,1 DexClouder Academy ProActivist Bonus
- %0,1 DexClouder Activist Bonus
- %0,1 DexClouder Academy Activist Bonus
- %0,1 DexClouder Beauty Bonus


### What are the PEP (Parex Request Contract) Types

- `PEP-2 (Token)` 

### Where Can I Run parex Node?
You can run parex Node on
- `Amazon Web Services`
- `Azure`
- `Google Cloud`
- `Your Own Server/Desktop`

### What are the transaction status ?
- `Success` 
- `Pending` 
- `Fail`

### MasterTracker requirements;
(Only vaild after 01/05/2021 purchases)
- `Each DexMining Package must be attached to 1 DexTracker.`
- `Each Master Package must be attached to 1 MasterTracker.`
- `MasterTracker ServiceFee range is (%5-%50)`
- `DexTracker revenues will be given hourly.`

### Miner requirements;
- `Minimum %90 Sync.`

### Parex Mining Calculating

|  ~      | Max      | Min      | Avg      |
|:-------:|:--------:|:--------:|:--------:|
| Hourly  | 0.323    | 0.233    | 0.278    |
| Daily   | 7.752    | 5.590    | 6.671    |
| Monthly | 232.560  | 167.700  | 200.130  |
| Yearly  | 2790.720 | 2012.400 | 2401.560 |

### How Can I Update to the Latest parex Version?
Run the command on Current DockerHost:

```
service docker start
```

```
docker kill parex 
docker pull parex/parex
docker run -d --rm -p 2020:2020 -p 2053:3030 -v parex:/var/lib/postgresql/ --privileged --log-driver=none --name parex parex/parex:latest
```


### Common Problems
These options are settings that change shell behavior. The following table is a list of options that might be useful to you:

| Check | How         | 
| :---: | :---------- | 
| Cannot connect to the Docker daemon. Is the docker daemon running on this host?  | Check your docker service is up and running.|
| Block Sync is not working  | Check your internet connectivity. |


### How to Backup the parex Node?

MyDexCahin maps blocks inside PostgreSQL and it has been addressed inside dockerfile. All the data is saved inside **`/var/lib/docker/volumes/parex`** and make sure that you **backup** the folder.


#### Linux & MacOs

##### 1. Stop `parex` Node Docker Container (For Data Consistency):

``` 
docker kill parex
```

##### 2. Copy `/var/lib/docker/volumes/parex` to Backup Path:

``` 
rsync -avzhHP /var/lib/docker/volumes/parex/ /backup_path/parex/
```

##### 3. Start `parex` Docker Container on the New Docker Host :

``` 
docker run -d --rm -p 2020:2020 -p 2053:3030 -v parex:/var/lib/postgresql/ --privileged --log-driver=none --name parex parex/parex:latest
```


##### 4. Follow the Blocks :

``` 
docker attach parex
```

#### Windows 

##### 1. Stop `parex` Node Docker Container (For Data Consistency):

``` 
docker kill parex
```

##### 2. Copy `%USERPROFILE%\AppData\Local\Docker\wsl\data\ext4.vhdx` to Backup Path:

##### 3. Start `parex` Docker Container on the New Docker Host :

``` 
docker run -d --rm -p 2020:2020 -p 2053:3030 -v parex:/var/lib/postgresql/ --privileged --log-driver=none --name parex parex/parex:latest
```


##### 4. Follow the Blocks :

``` 
docker attach parex
```


### How to Migrate the parex Node to Another Docker Host?
:warning: Before migrating your node be sure that docker is `installed on target`.

#### Linux & MacOs

##### 1. Stop `parex` Node Docker Container:

``` 
docker kill parex
```

##### 2. Copy Node Files to New Docker Host :

``` 
rsync -avzhHP --rsync-path="sudo rsync" -e "ssh -i key -o StrictHostKeyChecking=no" /var/lib/docker/volumes/parex/ root@target_ip:/var/lib/docker/volumes/parex/
```

##### 3. Start `parex` Docker Container on the New Host :

``` 
docker run -d --rm -p 2020:2020 -p 2053:3030 -v parex:/var/lib/postgresql/ --privileged --log-driver=none --name parex parex/parex:latest
```

##### 4. Follow the Blocks on the New Docker Host :

``` 
docker attach parex
```

#### Windows

##### 1. Stop `parex` Node Docker Container:

``` 
docker kill parex
```

##### 2. Copy Node Files to New Docker Host :

``` 
%USERPROFILE%\AppData\Local\Docker\wsl\data\ext4.vhdx --> to the new dockerhost
```

##### 3. Start `parex` Docker Container on the New Host :

``` 
docker run -d --rm -p 2020:2020 -p 2053:3030 -v parex:/var/lib/postgresql/ --privileged --log-driver=none --name parex parex/parex:latest
```


##### 4. Follow the Blocks on the New Docker Host :

``` 
docker attach parex
```

### I am Getting Errors in Windows OS? 
Make sure `Use the WSL 2 based engine` is enabled in Docker General Settings.


### Where is the Docker Mount Volume Located in Windows OS? 
Mount folder is located under:

``` 
\\wsl$\docker-desktop-data\version-pack-data\community\docker\volumes
```

### Where is the Pyhsical Path Docker Mount Volume Located in Windows OS? 
Mount disk is located under:

``` 
%USERPROFILE%\AppData\Local\Docker\wsl\data\ext4.vhdx
```
### How to run Test Mode 
Test mode is used for making demo for DexChain Network. **Do not use for production!**
```
docker run -d --rm -p 2020:2020 -p 2053:3030 -v parex:/var/lib/postgresql/ --privileged --log-driver=none --name parextestnet parex/parex:testnet
```


### Help! It's not working for me!

No problem. Reach out to us by [opening an issue](https://github.com/parex/parex/issues/new)


## Roadmap

- We are hardly working on new features:
  - `Cloud Market Deployments`

---

[![Twitter](https://img.shields.io/twitter/follow/parextech?style=social)](https://twitter.com/parextech)
