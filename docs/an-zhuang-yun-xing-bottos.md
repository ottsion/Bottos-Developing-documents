# Installation and operation of Bottos

> Difference: A single node is generally used to start a single node locally for contract development and testing, and is not connected to other nodes, generally reserving the default configuration. Multiple nodes connect to the Bottos main network or test network. It can also be used to make use of a small private network. There are general needs for basic configuration.

## Start single node

- Enter the directory where `GOPATH` is located

```
cd  ~/go/src/github.com/
```

- Download the project and decompress it

```
wget https://github.com/bottos-project/bottos/releases/download/tag_bottos3.2/bottos.tar.gz
tar zxvf bottos.tar.gz
cd bottos
```

- Start Bottos single node

```
./bottos --delegate=bottos
```

- `--delegate`:Specify the Account of the block producer

If the following information is returned, the node will start successfully.

```
CommitBlock by p2p: lib: 1
InsertBlock: number:1, delegate:bottos, trxn:0, time=1537948299, hash: 566fb29ab982c128bf6c71297bc4e7d558e0f86ae89a7f3955ea46b04689fb5a, prevHash=caf2bae84f70412354211dd5028142eca6901b06b9a65dfbe9df065bcf56e291
CommitBlock by p2p: lib: 2
InsertBlock: number:2, delegate:bottos, trxn:0, time=1537948302, hash: 8abe6aef22249ab58d6c7cd3970f909571c4e818f3757d9de7d86870bfc7465b, prevHash=566fb29ab982c128bf6c71297bc4e7d558e0f86ae89a7f3955ea46b04689fb5a
```

## Connect to test network

Connect the above initiated single node to the Bottos test network. The following configuration is required.

Modify `config-testnet.toml` file

- P2PServAddr:Modify the external network IP of the current node

```
P2PServAddr = "192.168.1.1"   // Modify the external network IP of the current node
```

Then run the following command to connect the current node to the test network.

Note: if there is a dataDir cache directory in the project directory, we first need to run the following command to delete the cache.

```
rm -rf datadir
```

Start node, connect to test network

```
./bottos --config="./config-testnet.toml" --genesis="./genesis-testnet.toml"
```

In a moment, if a large number of the following printed information appears, it indicates that the automatic synchronization block has been successfully connected to the test network

```
CommitBlock by p2p: lib: 1
InsertBlock: number:1, delegate:bottos, trxn:0, time=1537888767, hash: 03f6c7aa72314be76902b6c2d4b86b7afbb07d2b4b4dec67caf6fc51e125e9ed, prevHash=98128aa21d634eda9cb0152314b06480d4c51b0bf18ea6d39f5189388e1bf4ee
CommitBlock by p2p: lib: 2
InsertBlock: number:2, delegate:bottos, trxn:0, time=1537888770, hash: c87a1c59aaa87f890169a1016931b3a9e539e72e475c0861623ed36fbd00c1b4, prevHash=03f6c7aa72314be76902b6c2d4b86b7afbb07d2b4b4dec67caf6fc51e125e9ed
CommitBlock by p2p: lib: 3
InsertBlock: number:3, delegate:bottos, trxn:0, time=1537888773, hash: 3bcf9ecf116891b226b2c6b31578d5f1ee867a75b667752286eeaf3d237e684b, prevHash=c87a1c59aaa87f890169a1016931b3a9e539e72e475c0861623ed36fbd00c1b4
CommitBlock by p2p: lib: 4
```