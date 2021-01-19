# Welcome to Libo Explorer Documentation

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
