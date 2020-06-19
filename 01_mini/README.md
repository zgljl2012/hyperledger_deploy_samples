# Test

```bash

make clean

make crypto

make genesis

make up

make cli

```

启动 explorer：

```bash

make install-chain-code

# 需要修改 explorer/connection-profile/first-network.json 中的 admin user 的 keystore

make dashboard

```

details of install-chain-code

```bash

# 创建 channel
peer channel create -o orderer.example.com:7050 -c mychannel -f ./channel-artifacts/mychannel.tx

# peer 加入 channel
peer channel join -b mychannel.block

# 安装智能合约
peer chaincode install -n mycc -p github.com/hyperledger/fabric/singlepeer/chaincode/go/example02/cmd/ -v 1.0

# 实例化智能合约
peer chaincode instantiate -o orderer.example.com:7050 -C mychannel -n mycc -v 1.0 -c '{"Args":["init","a","100","b","200"]}' -P "AND ('Org1MSP.peer')"

# query 查询 a
peer chaincode query -C mychannel -n mycc -c '{"Args":["query","a"]}'

# invoke 一笔 a 向 b 转 10 的交易
peer chaincode invoke -C mychannel -n mycc -c '{"Args":["invoke","a","b","10"]}'

# 在查一次 a 和 b
peer chaincode query -C mychannel -n mycc -c '{"Args":["query","a"]}'
peer chaincode query -C mychannel -n mycc -c '{"Args":["query","b"]}'

# 查看当前块号
peer channel getinfo -c mychannel

```
