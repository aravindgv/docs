DSP Node
========
## Hardware Requirements

## Prerequisites
### Linux
```bash
sudo su -
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash
export NVM_DIR="${XDG_CONFIG_HOME/:-$HOME/.}nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
nvm install 10
nvm use 10
exit
```

#### Ubuntu/Debian
```bash
sudo apt install -y make cmake build-essential python
```

#### Centos/Fedora/AWS Linux:
```bash
sudo yum install -y make cmake3 python
```

## Install
```bash
sudo su -
nvm use 10
npm install -g pm2
npm install -g @liquidapps/dsp --unsafe-perm=true
exit
```
## Configuration
```bash
sudo su -
setup-dsp
systemctl stop dsp
systemctl start dsp
systemctl enable dsp
exit
```

And fill in the following details:
### Demux Backend
DEMUX_BACKEND 

- state_history_plugin 
- zmq_plugin - only if using nodeos with eosrio's version of the ZMQ plugin: https://github.com/eosrio/eos_zmq_plugin

### IPFS Cluster
IPFS_HOST - ipfs hostname
IPFS_PORT (5001) - ipfs port
IPFS_PROTOCOL (http) - ipfs protocol

hostname, port and protocol of [IPFS Cluster](ipfs-cluster)


### DSP Account
DSP_ACCOUNT and DSP_PRIVATE_KEY - Account and private key of [Generated DSP Account](dsp-account)

### nodeos ENVS
[EOS Node Settings](eosio-node)

NODEOS_HOST - nodeos hostname

NODEOS_PORT (8888) - nodeos port 

NODEOS_ZMQ_PORT (5557) - if using zmq_plugin

NODEOS_WEBSOCKET_PORT (8887) - if using state_history_plugin

NODEOS_CHAINID:

 - mainnet chainID: aca376f206b8fc25a6ed44dbdc66547c36c6c33e3a119ffbeaef943642f0e906
 - kylin chainID: 5fff1dae8dc8e2fc4d5b23b2c7665c97f9e9d8edf2b6485a86ba311c25639191


## Check logs
```bash
sudo pm2 logs
```

output should look like:
```
1|demux    | demux listening on port 3195!
1|demux    | ws connected
1|demux    | got abi
0|dapp-services-node  | services listening on port 3115!
0|dapp-services-node  | service node webhook listening on port 8812!
2|ipfs-dapp-service-node  | ipfs listening on port 13115!
2|ipfs-dapp-service-node  | commited to: ipfs://zb2rhmy65F3REf8SZp7De11gxtECBGgUKaLdiDj7MCGCHxbDW
2|ipfs-dapp-service-node  | ipfs connection established
```
