
.PHONY: explorer

down:
	@docker-compose down -v

clean: down
	@rm -rf channel-artifacts
	@rm -rf crypto-config

crypto:
	@mkdir -p crypto-config
	@docker run --rm -it -v `pwd`:/multipeer hyperledger/fabric-tools:1.4.3 cryptogen generate --config=/multipeer/crypto-config.yaml --output=/multipeer/crypto-config/

genesis:
	@mkdir -p channel-artifacts
	# 生成创世块
	@docker run --rm -it -v `pwd`:/multipeer hyperledger/fabric-tools:1.4.3 configtxgen -profile OneOrgsOrdererGenesis -outputBlock /multipeer/channel-artifacts/genesis.block -channelID system -configPath /multipeer/
	# 生成通道配置区块
	@docker run --rm -it -v `pwd`:/multipeer hyperledger/fabric-tools:1.4.3 configtxgen -profile OneOrgsChannel -outputCreateChannelTx /multipeer/channel-artifacts/mychannel.tx -channelID mychannel -configPath /multipeer/

up:
	# start orderer
	@docker-compose up -d orderer.example.com peer0.org1.example.com cli

explorer:
	@docker-compose up explorer

cli:
	@docker exec -it 01_mini_cli_1 /bin/bash
