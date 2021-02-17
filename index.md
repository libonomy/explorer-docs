---
layout: default
---

<!-- [Document](docs/CODE_OF_CONDUCT.md)
[Home](./Home.md). -->

# Libonomy Documentation

Libo Explorer is a Block Explorer and Analytics Platform for Libo Coin, a decentralized smart contracts platform.

## Setting Up Mainnet Node and Rest Server

This document will guide you on setting up the libonomy node and connecting it
over to the current mainnet-stake release.
Important: Due the release of new features of mainnet such as P2P AI Protocol,
Inter Neural Smart contract VM or INSC VM , BTC, ETH and COSMOS relay, the
chain of the mainnet will chain to further versions,
The development team of libonomy will provide the version of mainnet chain
before the the upgrade occurs,

```diff
- Kindly don't try to run validator nodes without developers consultation , the validator nodes
- include the AI model configuration which stands out of the scope of this documentation and
- integration, as AI model is meant for core configurations not for normal community usage.
```

###### For the sake of simplicity, we haven't explained the overall working of the consensus system that is staking , AI and Neural Consensus . Refer to Whitepaper for general understanding

[Libonomy Whitepaper](https://libonomy.com/assets/pdf/white-paper-libonomy-v2.0.pdf)

```diff
- Important Denomination:
- 1LBY = 1*10^6 flby
- 1PSIX= 1*10^6 fpsix

```

###### In case of any issues feel free to communicate in the group or via email or through our public channels

## Public REST NODE

###### In case you want to utilize the libonomy’s public nodes, you can use the urls given below.

[`http://18.232.124.100:26658/status`](http://18.232.124.100:26658/status) (for aphelion stake module
related RPC)

[`http://18.232.124.100:1318/status`](http://18.232.124.100:1318/status) (for SDK REST Server)

**REST ENDPOINTS INITIAL**

[REST API'S](https://documenter.getpostman.com/view/7412271/TVt18Pmj)

###### For JS library kindly utilize

[cuspstakeJS NPM](https://www.npmjs.com/package/@libonomy/cuspstakejs)

###### For JS library kindly utilize

[liboexplorer.com](http://liboexplorer.com/)

## Install Go

Install go by official repository version should be above 0.1.12.

Make sure that your gopath is set correctly and the bin is located on the path. E.g

```
mkdir -p $HOME/go/bin
echo "export PATH=$PATH:$(go env GOPATH)/bin" >> ~/.bash_profile
source ~/.bash_profile
```

#### Installing the services

```
git clone https://github.com/libonomy/cusp
```

#### Enter the directory

```
cd cusp/
```

#### In the Cusp Director point to the latest release i.e

```
git checkout v1.0.0
```

#### After switching to the latest release, install the required dependencies,

```
make install
```

```diff
-In case of error , install build dependencies
sudo apt update
sudo apt install build-essential
sudo apt-get install manpages-dev
```

#Make sure you are running correct version by using command

```
sudo apt update
sudo apt install build-essential
sudo apt-get install manpages-dev
```

```
#It should give you the version 1.0.0
```

#### Running the daemon service and connecting through cli to execute commands

#### From anywhere within your system after installing the services

This command will reset all previous configurations for safe configuration to the mainnet

```diff
-The chain that you are trying to connect to should be main-stake unless the development team
-announces the new version of chain. Always keep your node up to date.
```

1. Run cuspd unsafe-reset-all
2. Copy the genesis.json to the ~/.cuspd/config/ director
   If any genesis already exist replace it with this one
3. Within ~/.cuspd/config/ directory open config.toml
4. Edit line#16 by assigning name to your node
5. Within config.toml file, in the section [p2p] edit line#171
   persistent_peers and add the peers given below.
   Add persistent peers
   43f7bb1671db3ead72a9943efba102087a593480@18.232.124.100:26656
6. Use screen session to run daemon in the background or
   configure using systemd
7. After all is done run cuspd start
   Your node is now connected to mainnet

Remember: Checksum for genesis.json is
91e7cab91704c2e88db079a690d3ff3c171e27df17fac38851b298ea651
059fc

#### Setting up the CLI for interaction

```
cuspcli config node http://127.0.0.1:26657 or use tcp
```

**#As you are on local network so config your CLI Flag to true as**

```
cuspcli config trust-node true
```

**#configure the chain-id**

```
cuspcli config chain-id main-stake
```

#### For setting up the rest/rpc service of node

```
cuspcli rest-server --chain-id=main-stake
--laddr=tcp://localhost:1317 --node
tcp://localhost:26657
```

```diff
-When running the rest node for public access, you need to
-allow cors by setting up reverse proxy using nginx or any
-other service for REST server. You can enable for aphelion
-stake module cors policy within ~/.cuspd/config/config.toml
-and edit line#85 and set “*” within cors_allowed_origins =["*"]
```

#### CLI Commands

#All the addresses begin with **bonomy** prefix

#For keypair generation

```
cuspcli keys add accountname
```

#the returned seed phrase and private key should be secured properly otherwise they will not
be recoverable

```
#for keys recovery from backup
cuspcli keys add --recover

#for checking keys
Cuspcli keys show accountname

#for all present keys in the node
cuspcli keys list

#for checkout account balance
Cuspcli query account accountname

#for sending coins from one account to another
cuspcli tx send senderaccountaddress receiveraccountaddress
9999999libocoin --chain-id=main-stake

#if you dont want to broadcast the transaction simply add
the flag --dry-run
```

#### For generation of multi sig keys

```
cuspcli keys add --multisig=key1,key2,key3[...]
--multisig-threshold=K new_key_name
```

```
#threshhold means the private keys set to sign the
transactions. All the keys which are going to be included
for multisign must also exist in local DB of system
```

#### View Transactions through CLI

```
#query txs on the basis of events

cuspcli query txs
--events='message.sender=libonomy1r6lr2mjgqczkprglwq3a2ve0j
n37udrwh5r9s9'

#pagination is supported by adding flags --page=1
--limit=10

#for multiple events just add &mention_your_event_name
```

#### Offline Transactions through CLI

```
# Using cuspcli you can simulate unsignedTX by following
example

cuspcli tx send <sender_address> <destination_address>
10flby --chain-id=<chain_id> --dry-run

#pagination is supported by adding flags --page=1
--limit=10

# for multiple events just add &mention_your_event_name

# to generate JSON output without broadcasting using cli
cuspcli tx send <sender_address> <recipient_address> 10flby
--chain-id=<chain_id> --generate-only > unsignedTx.json

#you can sign json raw tx with your key and output the
signed transaction
cuspcli tx sign --chain-id=<chain_id>
--from=<acount_name> unsignedTx.json > signedTx.json

#In order to validate the output
cuspcli tx sign --validate-signatures signedTx.json

#For broadcasting using cli
cuspcli tx broadcast --node=<node_URI> signedTx.json

#from REST URL kindly refer to our cuspstakejs package

#Or send post request toe REST_URL/txs

And in body send the signed transaction object

BODY:
 {
 "tx": {
 "msg": stdSignMsg.json.msgs,
 "fee": stdSignMsg.json.fee,
 "signatures": [
 {
"account_number":
stdSignMsg.json.account_number,
"sequence":
stdSignMsg.json.sequence,
 "signature": signatureBase64,
 "pub_key": {
 "type":
"aphelion/PubKeySecp256k1",
 "value":
getPubKeyBase64(ecpairPriv)
 }
 }
 ],
 "memo": stdSignMsg.json.memo
 },
 "mode": modeType //async or sync
}

```

#### In case to learn more about transaction signing utilize the NPM library examples or ontact us. All the necessary things are already shared
