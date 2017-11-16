# puppeth-tutorial

### Environments
- [geth](https://github.com/karalabe/go-ethereum/tree/puppeth-devcon3)
- [go 1.9](https://github.com/golang/go/wiki/Ubuntu)
- solc 0.4.18


### 1. setup
```bash
# build geth
$ cd go-ethereum
$ make all # go-client/build/bin/puppeth is generated

# make directories
$ mkdir -p testnet/{node1,node2}

# create 2 nodes with its own account
$ geth --datadir testnet/node1 account new
$ geth --datadir testnet/node2 account new

# run puppeth with datadir
$ puppeth --network testnet
```


### 2. configure genesis file
```bash
What would you like to do? (default = stats)
 1. Show network stats
 2. Configure new genesis
 3. Track new remote server
 4. Deploy network components
> 2

Which consensus engine to use? (default = clique)
 1. Ethash - proof-of-work
 2. Clique - proof-of-authority
> 1

Which accounts should be pre-funded? (advisable at least one)
> 0x4bc519d7950ff7cdd9a32b7eeed5992575027aab # from node1
> 0x71dd2bd8050ea5860a8967acff89db5936190462 # from node2
> 0x

Specify your chain/network ID if you want an explicit one (default = random)
> ENTER

Anything fun to embed into the genesis block? (max 32 bytes)
> ENTER

What would you like to do? (default = stats)
 1. Show network stats
 2. Manage existing genesis
 3. Track new remote server
 4. Deploy network components
> 2

 1. Modify existing fork rules
 2. Export genesis configuration
> 2

Which file to save the genesis into? (default = testnet.json)
> ENTER
INFO [11-15|02:06:10] Exported existing genesis block

```


### 3. run 2 geth clients
```bash
$ geth --datadir testnet/node1 init testnet.json
$ geth --datadir testnet/node2 init testnet.json
# terminal 1
$ geth --datadir testnet/node1 --port 3001
# terminal 2
$ geth --datadir testnet/node2 --port 3002
```

### 4. attach two geth client
```bash
# terminal 3
$ geth attach testnet/node1/geth.ipc
# terminal 4
$ geth attach testnet/node2/geth.ipc

```

### refs
https://modalduality.org/posts/puppeth/
https://blog.ethereum.org/2017/04/14/geth-1-6-puppeth-master/

### Errors

#### 1. command not found: docker
https://stackoverflow.com/a/9993668
https://apple.stackexchange.com/questions/271948/setup-config-of-ssh-macos
PATH=/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin
