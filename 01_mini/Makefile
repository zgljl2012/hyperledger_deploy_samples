
clean:
	@rm -rf channel-artifacts
	@rm -rf crypto-config

crypto:
	@mkdir -p crypto-config
	@docker run --rm -it -v `pwd`:/multipeer hyperledger/fabric-tools cryptogen generate --config=/multipeer/crypto-config.yaml --output=/multipeer/crypto-config/

genesis:
	@mkdir -p channel-artifacts
	# 生成创世块
	@docker run --rm -it -v `pwd`:/multipeer hyperledger/fabric-tools configtxgen -profile OneOrgsOrdererGenesis -outputBlock /multipeer/channel-artifacts/genesis.block -channelID system -configPath /multipeer/
	# 生成通道配置区块
	@docker run --rm -it -v `pwd`:/multipeer hyperledger/fabric-tools configtxgen -profile OneOrgsChannel -outputCreateChannelTx /multipeer/channel-artifacts/mychannel.tx -channelID mychannel -configPath /multipeer/

up:
	# start orderer
	@docker-compose up cli

dashboard:
	@docker-compose up explorer

install-chain-code:
	@docker-compose up install-chain-code

cli:
	@docker exec -it singlepeer_cli_1 /bin/bash

down:
	@docker-compose down -v
