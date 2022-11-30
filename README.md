# Parex

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

Commands to Execute: For Moving from old Node to new Node
```
wget https://raw.githubusercontent.com/parexmarket/parex/main/movetoparex.sh
```
```
bash movetoparex.sh
```




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
- parex Node Offline Sync (Fastest Way) https://backup.parexscan.io
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
- Mining
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



### Parex Mining Calculating

|  ~      | Max      | Min      | Avg      |
|:-------:|:--------:|:--------:|:--------:|
| Hourly  | 0.323    | 0.233    | 0.278    |
| Daily   | 7.752    | 5.590    | 6.671    |
| Monthly | 232.560  | 167.700  | 200.130  |
| Yearly  | 2790.720 | 2012.400 | 2401.560 |


## Roadmap

- We are hardly working on new features:
  - `Cloud Market Deployments`

---

[![Twitter](https://img.shields.io/twitter/follow/parextech?style=social)](https://twitter.com/parextech)
