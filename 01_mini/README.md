# Test

```bash

make clean

make crypto

make genesis

make up

```

## 创建 Channel, 部署合约

进入 cli

```bash

make cli

```

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

exit

```

## Explorer

复制好 admin 的 key 路径后，启动 explorer：

```bash

# 需要修改 explorer/connection-profile/first-network.json 中的 admin user 的 keystore
# 仅需修改：`adminPrivateKey.path` 这一项，修改为自己生成的文件名
# admin keystore 位于：./crypto-config/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp/keystore/0ee4c7cb3a097b5b1ab58342615862f980a3f44b6dc79d491a4b1d0afbc0c9d6_sk

# 仅需修改目录最后一层的文件名，`0ee4c7cb3a097b5b1ab58342615862f980a3f44b6dc79d491a4b1d0afbc0c9d6_sk`
make explorer

```

启动后，访问：[localhost](http://127.0.0.1:8080)，用户名密码：`amdin`, `password`
