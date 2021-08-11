[TOC]
# JSON-RPC Server
## 参考资料
- `https://eth.wiki/json-rpc/API`
- `https://etclabscore.github.io/core-geth/JSON-RPC-API/modules/personal`

## 交易类型支持
只支持ethereum的LegacyTxType类型交易，不支持AccessListTxType和DynamicFeeTxType类型交易。

## JSON-RPC Methods
|                 Method                 | Namespace | Implemented |        Notes         |
| ------------------------------------- | -------- | ---------- | ------------------- |
| `web3_clientVersion`                    | Web3      | ✔          |                     |
| `web3_sha3`                            | Web3      | ✔          |                     |
| `net_version`                          | Net       | ✔          |                     |
| `net_peerCount`                         | Net       | ✔          | mock，非真实P2P连接数  |
| `net_listening`                         | Net       | ✔          |                     |
| `eth_protocolVersion`                   | Eth       |            |                     |
| `eth_syncing`                          | Eth       |            |                     |
| `eth_gasPrice`                         | Eth       | ✔          |                     |
| `eth_accounts`                         | Eth       | ✔          |                     |
| `eth_blockNumber`                       | Eth       | ✔          |                     |
| `eth_getBalance`                        | Eth       | ✔          |                     |
| `eth_getStorageAt`                      | Eth       | ✔          |                     |
| `eth_getTransactionCount`                | Eth       | ✔          |                     |
| `eth_getBlockTransactionCountByNumber`    | Eth       | ✔          |                     |
| `eth_getBlockTransactionCountByHash`      | Eth       | ✔          |                     |
| `eth_getCode`                          | Eth       | ✔          |                     |
| `eth_sign`                             | Eth       | ✔          |                     |
| `eth_sendTransaction`                   | Eth       | ✔          |                     |
| `eth_sendRawTransaction`                 | Eth       | ✔          |                     |
| `eth_call`                             | Eth       | ✔          |                     |
| `eth_estimateGas`                       | Eth       | ✔          |                     |
| `eth_getBlockByNumber`                  | Eth       | ✔          |                     |
| `eth_getBlockByHash`                    | Eth       | ✔          |                     |
| `eth_getTransactionByHash`               | Eth       | ✔          |                     |
| `eth_getTransactionByBlockHashAndIndex`   | Eth       | ✔          |                     |
| `eth_getTransactionReceipt`              | Eth       | ✔          |                     |
| `eth_newFilter`                         | Eth       | ✔          |                     |
| `eth_newBlockFilter`                    | Eth       | ✔          |                     |
| `eth_newPendingTransactionFilter`         | Eth       | ✔          |                     |
| `eth_uninstallFilter`                   | Eth       | ✔          |                     |
| `eth_getFilterChanges`                  | Eth       | ✔          |                     |
| `eth_getLogs`                          | Eth       | ✔          |                     |
| `eth_getTransactionbyBlockNumberAndIndex` | Eth       |             |                     |
| `eth_getWork`                          | Eth       |             |                     |
| `eth_submitWork`                        | Eth       |             |                     |
| `eth_submitHashrate`                    | Eth       |             |                     |
| `eth_getCompilers`                      | Eth       |             |                     |
| `eth_compileLLL`                        | Eth       |             |                     |
| `eth_compileSolidity`                   | Eth       |             |                     |
| `eth_compileSerpent`                    | Eth       |             |                     |
| `eth_signTransaction`                   | Eth       | ✔          |                     |
| `eth_mining`                           | Eth       | N/A         | Not relevant to Mondo |
| `eth_coinbase`                         | Eth       | N/A         | Not relevant to Mondo |
| `eth_hashrate`                         | Eth       | N/A         | Not relevant to Mondo |
| `eth_getUncleCountByBlockHash`           | Eth       | N/A         | Not relevant to Mondo |
| `eth_getUncleCountByBlockNumber`         | Eth       | N/A         | Not relevant to Mondo |
| `eth_getUncleByBlockHashAndIndex`         | Eth       | N/A         | Not relevant to Mondo |
| `eth_getUncleByBlockNumberAndIndex`       | Eth       | N/A         | Not relevant to Mondo |
| `eth_subscribe`                         | Websocket | ✔          | todo                 |
| `eth_unsubscribe`                       | Websocket | ✔          | todo                 |
| `personal_deriveAccount`                 | Personal  | ✔          |                     |
| `personal_ecRecover`                    | Personal  | ✔          |                     |
| `personal_importRawKey`                 | Personal  | ✔          |                     |
| `personal_initializeWallet`              | Personal  | ✔          |                     |
| `personal_listAccounts`                 | Personal  | ✔          |                     |
| `personal_listWallets`                  | Personal  | ✔          |                     |
| `personal_lockAccount`                  | Personal  | ✔          |                     |
| `personal_newAccount`                   | Personal  | ✔          |                     |
| `personal_openWallet`                   | Personal  |            |                     |
| `personal_unlockAccount`                 | Personal  | ✔          |                     |
| `personal_sendTransaction`               | Personal  | ✔          |                     |
| `personal_sign`                         | Personal  | ✔          |                     |
| `personal_signAndSendTransaction`         | Personal  | ✔          |                     |
| `personal_signTransaction`               | Personal  | ✔          |                     |
| `personal_unpair`                         | Personal  |            |                     |
| `db_putString`                         | DB        |             |                     |
| `db_getString`                         | DB        |             |                     |
| `db_putHex`                            | DB        |             |                     |
| `db_getHex`                            | DB        |             |                     |
| `shh_post`                             | SSH       |             |                     |
| `shh_version`                          | SSH       |             |                     |
| `shh_newIdentity`                       | SSH       |             |                     |
| `shh_hasIdentity`                       | SSH       |             |                     |
| `shh_newGroup`                         | SSH       |             |                     |
| `shh_addToGroup`                        | SSH       |             |                     |
| `shh_newFilter`                         | SSH       |             |                     |
| `shh_uninstallFilter`                   | SSH       |             |                     |
| `shh_getFilterChanges`                  | SSH       |             |                     |
| `shh_getMessages`                       | SSH       |             |                     |
| `admin_addPeer`                         | Admin     |             |                     |
| `admin_datadir`                         | Admin     |             |                     |
| `admin_nodeInfo`                        | Admin     |             |                     |
| `admin_peers`                          | Admin     |             |                     |
| `admin_startRPC`                        | Admin     |             |                     |
| `admin_startWS`                         | Admin     |             |                     |
| `admin_stopRPC`                         | Admin     |             |                     |
| `admin_stopWS`                         | Admin     |             |                     |
| `clique_getSnapshot`                    | Clique    |             |                     |
| `clique_getSnapshotAtHash`               | Clique    |             |                     |
| `clique_getSigners`                     | Clique    |             |                     |
| `clique_proposals`                      | Clique    |             |                     |
| `clique_propose`                        | Clique    |             |                     |
| `clique_discard`                        | Clique    |             |                     |
| `clique_status`                         | Clique    |             |                     |
| `debug_backtraceAt`                     | Debug     |             |                     |
| `debug_blockProfile`                    | Debug     |             |                     |
| `debug_cpuProfile`                      | Debug     |             |                     |
| `debug_dumpBlock`                       | Debug     |             |                     |
| `debug_gcStats`                         | Debug     |             |                     |
| `debug_getBlockRlp`                     | Debug     |             |                     |
| `debug_goTrace`                         | Debug     |             |                     |
| `debug_memStats`                        | Debug     |             |                     |
| `debug_seedHash`                        | Debug     |             |                     |
| `debug_setHead`                         | Debug     |             |                     |
| `debug_setBlockProfileRate`              | Debug     |             |                     |
| `debug_stacks`                         | Debug     |             |                     |
| `debug_startCPUProfile`                 | Debug     |             |                     |
| `debug_startGoTrace`                    | Debug     |             |                     |
| `debug_stopCPUProfile`                  | Debug     |             |                     |
| `debug_stopGoTrace`                     | Debug     |             |                     |
| `debug_traceBlock`                      | Debug     |             |                     |
| `debug_traceBlockByNumber`               | Debug     |             |                     |
| `debug_traceBlockByHash`                 | Debug     |             |                     |
| `debug_traceBlockFromFile`               | Debug     |             |                     |
| `debug_standardTraceBlockToFile`         | Debug     |             |                     |
| `debug_standardTraceBadBlockToFile`       | Debug     |             |                     |
| `debug_traceTransaction`                 | Debug     |             |                     |
| `debug_verbosity`                       | Debug     |             |                     |
| `debug_vmodule`                         | Debug     |             |                     |
| `debug_writeBlockProfile`                | Debug     |             |                     |
| `debug_writeMemProfile`                 | Debug     |             |                     |
| `les_serverInfo`                        | Les       |             |                     |
| `les_clientInfo`                        | Les       |             |                     |
| `les_priorityClientInfo`                 | Les       |             |                     |
| `les_addBalance`                        | Les       |             |                     |
| `les_setClientParams`                   | Les       |             |                     |
| `les_setDefaultParams`                  | Les       |             |                     |
| `les_latestCheckpoint`                  | Les       |             |                     |
| `les_getCheckpoint`                     | Les       |             |                     |
| `les_getCheckpointContractAddress`        | Les       |             |                     |
| `miner_getHashrate`                     | Miner     |             |                     |
| `miner_setExtra`                        | Miner     |             |                     |
| `miner_setGasPrice`                     | Miner     |             |                     |
| `miner_start`                          | Miner     |             |                     |
| `miner_stop`                           | Miner     |             |                     |
| `miner_setEtherbase`                    | Miner     |             |                     |
| `txpool_content`                        | TXPool    |             |                     |
| `txpool_inspect`                        | TXPool    |             |                     |
| `txpool_status`                         | TXPool    |             |                     |

## RPC Methods

### web3
- web3_clientVersion
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"web3_clientVersion","params":[],"id":67}'

{"jsonrpc":"2.0","id":67,"result":"Geth/v1.10.3-stable/linux-amd64/go1.15.3"}
```

- web3_sha3
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"web3_sha3","params":["0x68656c6c6f20776f726c64"],"id":64}'

{"jsonrpc":"2.0","id":64,"result":"0x47173285a8d7341e5e972fc677286384f802f8ef42a5ec5f03bbfa254cb01fad"}
```

### net
- net_version
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"net_version","params":[],"id":67}'

{"jsonrpc":"2.0","id":67,"result":"1"}
```

- net_listening
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data  '{"jsonrpc":"2.0","method":"net_listening","params":[],"id":67}'

{"jsonrpc":"2.0","id":67,"result":true}
```

- net_peerCount
  返回的数据是mock的，并非真实的P2P连接数
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":74}'

{"jsonrpc":"2.0","id":74,"result":"0x1"}
```

### eth
- eth_protocolVersion 未支持
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_protocolVersion","params":[],"id":67}'

{"jsonrpc":"2.0","id":67,"error":{"code":-32601,"message":"the method eth_protocolVersion does not exist/is not available"}}
```

- eth_syncing 未支持
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_syncing","params":[],"id":1}'

{"jsonrpc":"2.0","id":1,"error":{"code":-32000,"message":"method handler crashed"}}
```

- eth_coinbase 未支持
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_coinbase","params":[],"id":64}'

{"jsonrpc":"2.0","id":64,"error":{"code":-32601,"message":"the method eth_coinbase does not exist/is not available"}}
```

- eth_mining 未支持
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_mining","params":[],"id":64}'

{"jsonrpc":"2.0","id":64,"error":{"code":-32601,"message":"the method eth_mining does not exist/is not available"}}
```

- eth_hashrate 未支持
```
```

- eth_gasPrice
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_gasPrice","params":[],"id":64}'

{"jsonrpc":"2.0","id":64,"result":"0xe8d4a51000"}
```

- eth_accounts
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_accounts","params":[],"id":1}'

{"jsonrpc":"2.0","id":1,"result":["0xb7ff5eee043afc5e27b4ff05c3a6bed5cd3b978d","0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f"]}
```

- eth_blockNumber
  Returns the number of most recent block.
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":83}'

{"jsonrpc":"2.0","id":83,"result":"0x19"}
```

- eth_getBalance
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_getBalance","params":["0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f", "latest"],"id":1}'

{"jsonrpc":"2.0","id":1,"result":"0x16345785d89adf7"}
```

- eth_getStorageAt
  Returns the value from a storage position at a given address. 如果参数是合约地址，就是取合约的字节码？？
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0", "method": "eth_getStorageAt", "params": ["0x295a70b2de5e3953354a6a8344e616ed314d7251", "0x0", "latest"], "id": 1}'

{"jsonrpc":"2.0","id":1,"result":"0x0000000000000000000000000000000000000000000000000000000000000000"}
```

- eth_getTransactionCount
  Returns the number of transactions sent from an address.
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_getTransactionCount","params":["0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f","latest"],"id":1}'

{"jsonrpc":"2.0","id":1,"result":"0x1"}
```

- eth_getBlockTransactionCountByHash
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_getBlockTransactionCountByHash","params":["0xF87F437A0C322EBD6A9F42FF2AFBF64C32D274A8C3A8606EE148E1BBA75B18BA"],"id":1}'

{"jsonrpc":"2.0","id":1,"result":"0x1"}
```

- eth_getBlockTransactionCountByNumber
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data  '{"jsonrpc":"2.0","method":"eth_getBlockTransactionCountByNumber","params":["0x3"],"id":1}'

{"jsonrpc":"2.0","id":1,"result":"0x1"}
```

- eth_getUncleCountByBlockHash mondo没有叔块概念，叔块的都不支持
```
```

- eth_getUncleCountByBlockNumber 叔块的都不支持
```
```

- eth_getCode
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data  '{"jsonrpc":"2.0","method":"eth_getCode","params":["0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f", "0x2"],"id":1}'

{"jsonrpc":"2.0","id":1,"result":"0x"}
```

- eth_sign
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data  '{"jsonrpc":"2.0","method":"eth_sign","params":["0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f", "0xdeadbeaf"],"id":1}'

{"jsonrpc":"2.0","id":1,"result":"0x2a61d3ad6cee5e083838bdef6c7ea4ff447727055b81da63001df7150d632ccb26697237f5a03a51306a0563572551c078af7d979665c67ac63d6ba3a810cc501c"}
```

- eth_signTransaction
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"id":1,"jsonrpc":"2.0","method":"eth_signTransaction","params":[{"nonce":"0x9323","data":"0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675","from":"0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f","gas":"0x76c0","gasPrice":"0xE8D4A51000","to":"0xd46e8dd67c5d32be8058bb8eb970870f07244567","value":"0x2540BE400"}]}'

tx details:
{
	"id": 1,
	"jsonrpc": "2.0",
	"method": "eth_signTransaction",
	"params": [{
		"nonce": "0x9323",
		"data": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675",
		"from": "0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f",
		"gas": "0x76c0",
		"gasPrice": "0xE8D4A51000",
		"to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
		"value": "0x2540BE400"
	}]
}

{
	"jsonrpc": "2.0",
	"id": 1,
	"result": {
		"raw": "0xf89682932385e8d4a510008276c094d46e8dd67c5d32be8058bb8eb970870f072445678502540be400a9d46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675820327a0b306cc4e6583e0e92e849339ea0c90f853d05eae2a80ac3f86e83e2e9d286355a07c9eff93975bcdb683144a274ecf57a541f903df3a98c0b5c965286b826895cd",
		"tx": {
			"type": "0x0",
			"nonce": "0x9323",
			"gasPrice": "0xe8d4a51000",
			"maxPriorityFeePerGas": null,
			"maxFeePerGas": null,
			"gas": "0x76c0",
			"value": "0x2540be400",
			"input": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675",
			"v": "0x327",
			"r": "0xb306cc4e6583e0e92e849339ea0c90f853d05eae2a80ac3f86e83e2e9d286355",
			"s": "0x7c9eff93975bcdb683144a274ecf57a541f903df3a98c0b5c965286b826895cd",
			"to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
			"hash": "0x5c26f679798c5ab5badb25f556aa6be5e7e2c8f4cf11e7cc96718cab8d787a8e"
		}
	}
}
```

- eth_sendRawTransaction
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data  '{"jsonrpc":"2.0","method":"eth_sendRawTransaction","params":["0xf89682932385e8d4a510008276c094d46e8dd67c5d32be8058bb8eb970870f072445678502540be400a9d46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675820327a0b306cc4e6583e0e92e849339ea0c90f853d05eae2a80ac3f86e83e2e9d286355a07c9eff93975bcdb683144a274ecf57a541f903df3a98c0b5c965286b826895cd"],"id":1}'

{"jsonrpc":"2.0","id":1,"result":"0x5c26f679798c5ab5badb25f556aa6be5e7e2c8f4cf11e7cc96718cab8d787a8e"}
```

- eth_sendTransaction
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_sendTransaction","params":[{"from":"0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f","to":"0xd46e8dd67c5d32be8058bb8eb970870f07244567","gas":"0x76c0","gasPrice":"0xE8D4A51000","value":"0xDE0B6B3A7640000","data":"0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"}],"id":1}'
{"jsonrpc":"2.0","id":1,"result":"0x8689082200f59f70541705cd7ffd8bf025776811f3b7fcc8ef476966930b6f20"}
```

- eth_call
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_call","params":[{"data":"0x70a082310000000000000000000000000f508f143e77b39f8e20dd9d2c1e515f0f527d9f","from":"0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f","gas":"0x76c0","gasPrice":"0x1","to":"0x67EbBA731DCd5b763F5699650920a637eDbBEb93","value":"0x0"},"latest"],"id":1}'

{"jsonrpc":"2.0","id":1,"result":"0x00000000000000000000000000000000000000000000000003da53a727a597c3"}
```

- eth_estimateGas
```
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_estimateGas","params":[{"from":"0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f", "to":"0x67EbBA731DCd5b763F5699650920a637eDbBEb93", "data":"0xa9059cbb00000000000000000000000078a415a367057d89598d1ea670819428d7417b99000000000000000000000000000000000000000000000000000000000000007b"}],"id":1}' -H "Content-Type: application/json" http://localhost:8545

{"jsonrpc":"2.0","id":1,"result":"0xf94c"}

```

- eth_getBlockByHash
```
{"jsonrpc":"2.0","id":1,"result":{"difficulty":"0x0","extraData":"0x","gasLimit":"0x76c0","gasUsed":"0x5498","hash":"0x07dd46d62f6a5e97290381a2f40c1ac201d4dcfa71d9ba7811ec2db1cb1872ac","logsBloom":"0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000","miner":"0xd63d14331b012d2e4a7ca104d56a9b13fdf5b8ef","mixHash":"0x0000000000000000000000000000000000000000000000000000000000000000","nonce":"0x0000000000000000","number":"0x8fc61d","parentHash":"0x56039a3a63b049ef5c841c335dac8a3543af901fdb8f5b7e08af99868b996fed","receiptsRoot":"0x80f52b3bf835875d38c17e299ab46ddad86a833b47769c18b1e14c0b6daa9237","sha3Uncles":"0x0000000000000000000000000000000000000000000000000000000000000000","size":"0x435","stateRoot":"0xcebec4f94cea5ac9fa7ed51bd0ebf44f58f96716c07588ecdf2e5b717fb15aac","timestamp":"0x61132684","totalDifficulty":"0x0","transactions":["0x5c26f679798c5ab5badb25f556aa6be5e7e2c8f4cf11e7cc96718cab8d787a8e"],"transactionsRoot":"0xe4df3b4f90ae951e2bb013aa706ef2c6e5e4997b448d4b3ee74bb5202358bdf7","uncles":[]}}

{
	"jsonrpc": "2.0",
	"id": 1,
	"result": {
		"difficulty": "0x0",
		"extraData": "0x",
		"gasLimit": "0x76c0",
		"gasUsed": "0x5498",
		"hash": "0x07dd46d62f6a5e97290381a2f40c1ac201d4dcfa71d9ba7811ec2db1cb1872ac",
		"logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
		"miner": "0xd63d14331b012d2e4a7ca104d56a9b13fdf5b8ef",
		"mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
		"nonce": "0x0000000000000000",
		"number": "0x8fc61d",
		"parentHash": "0x56039a3a63b049ef5c841c335dac8a3543af901fdb8f5b7e08af99868b996fed",
		"receiptsRoot": "0x80f52b3bf835875d38c17e299ab46ddad86a833b47769c18b1e14c0b6daa9237",
		"sha3Uncles": "0x0000000000000000000000000000000000000000000000000000000000000000",
		"size": "0x435",
		"stateRoot": "0xcebec4f94cea5ac9fa7ed51bd0ebf44f58f96716c07588ecdf2e5b717fb15aac",
		"timestamp": "0x61132684",
		"totalDifficulty": "0x0",
		"transactions": ["0x5c26f679798c5ab5badb25f556aa6be5e7e2c8f4cf11e7cc96718cab8d787a8e"],
		"transactionsRoot": "0xe4df3b4f90ae951e2bb013aa706ef2c6e5e4997b448d4b3ee74bb5202358bdf7",
		"uncles": []
	}
}
```

- eth_getBlockByNumber
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data  '{"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["0x8fc61d", true],"id":1}'

{
	"jsonrpc": "2.0",
	"id": 1,
	"result": {
		"difficulty": "0x0",
		"extraData": "0x",
		"gasLimit": "0x76c0",
		"gasUsed": "0x5498",
		"hash": "0x07dd46d62f6a5e97290381a2f40c1ac201d4dcfa71d9ba7811ec2db1cb1872ac",
		"logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
		"miner": "0xd63d14331b012d2e4a7ca104d56a9b13fdf5b8ef",
		"mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
		"nonce": "0x0000000000000000",
		"number": "0x8fc61d",
		"parentHash": "0x56039a3a63b049ef5c841c335dac8a3543af901fdb8f5b7e08af99868b996fed",
		"receiptsRoot": "0x80f52b3bf835875d38c17e299ab46ddad86a833b47769c18b1e14c0b6daa9237",
		"sha3Uncles": "0x0000000000000000000000000000000000000000000000000000000000000000",
		"size": "0x435",
		"stateRoot": "0xcebec4f94cea5ac9fa7ed51bd0ebf44f58f96716c07588ecdf2e5b717fb15aac",
		"timestamp": "0x61132684",
		"totalDifficulty": "0x0",
		"transactions": [{
			"blockHash": "0x80f52b3bf835875d38c17e299ab46ddad86a833b47769c18b1e14c0b6daa9237",
			"blockNumber": "0x8fc61d",
			"from": "0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f",
			"gas": "0x76c0",
			"gasPrice": "0xe8d4a51000",
			"hash": "0x5c26f679798c5ab5badb25f556aa6be5e7e2c8f4cf11e7cc96718cab8d787a8e",
			"input": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675",
			"nonce": "0x9323",
			"to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
			"transactionIndex": "0x0",
			"value": "0x2540be400",
			"type": "0x0",
			"v": "0x0",
			"r": "0x0",
			"s": "0x0"
		}],
		"transactionsRoot": "0xe4df3b4f90ae951e2bb013aa706ef2c6e5e4997b448d4b3ee74bb5202358bdf7",
		"uncles": []
	}
}
```

- eth_getTransactionByHash
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_getTransactionByHash","params":["0x5c26f679798c5ab5badb25f556aa6be5e7e2c8f4cf11e7cc96718cab8d787a8e"],"id":1}'

{
	"jsonrpc": "2.0",
	"id": 1,
	"result": {
		"blockHash": "0x80f52b3bf835875d38c17e299ab46ddad86a833b47769c18b1e14c0b6daa9237",
		"blockNumber": "0x8fc61d",
		"from": "0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f",
		"gas": "0x76c0",
		"gasPrice": "0xe8d4a51000",
		"hash": "0x5c26f679798c5ab5badb25f556aa6be5e7e2c8f4cf11e7cc96718cab8d787a8e",
		"input": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675",
		"nonce": "0x9323",
		"to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
		"transactionIndex": "0x0",
		"value": "0x2540be400",
		"type": "0x0",
		"v": "0x0",
		"r": "0x0",
		"s": "0x0"
	}
}
```

- eth_getTransactionByBlockHashAndIndex
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_getTransactionByBlockHashAndIndex","params":["0x80F52B3BF835875D38C17E299AB46DDAD86A833B47769C18B1E14C0B6DAA9237", "0x0"],"id":1}'

{
	"jsonrpc": "2.0",
	"id": 1,
	"result": {
		"blockHash": "0x80f52b3bf835875d38c17e299ab46ddad86a833b47769c18b1e14c0b6daa9237",
		"blockNumber": "0x8fc61d",
		"from": "0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f",
		"gas": "0x76c0",
		"gasPrice": "0xe8d4a51000",
		"hash": "0x5c26f679798c5ab5badb25f556aa6be5e7e2c8f4cf11e7cc96718cab8d787a8e",
		"input": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675",
		"nonce": "0x9323",
		"to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
		"transactionIndex": "0x0",
		"value": "0x2540be400",
		"type": "0x0",
		"v": "0x0",
		"r": "0x0",
		"s": "0x0"
	}
}
```

- eth_getTransactionByBlockNumberAndIndex
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_getTransactionByBlockNumberAndIndex","params":["0x8fc61d", "0x0"],"id":1}'

{
	"jsonrpc": "2.0",
	"id": 1,
	"result": {
		"blockHash": "0x80f52b3bf835875d38c17e299ab46ddad86a833b47769c18b1e14c0b6daa9237",
		"blockNumber": "0x8fc61d",
		"from": "0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f",
		"gas": "0x76c0",
		"gasPrice": "0xe8d4a51000",
		"hash": "0x5c26f679798c5ab5badb25f556aa6be5e7e2c8f4cf11e7cc96718cab8d787a8e",
		"input": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675",
		"nonce": "0x9323",
		"to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
		"transactionIndex": "0x0",
		"value": "0x2540be400",
		"type": "0x0",
		"v": "0x0",
		"r": "0x0",
		"s": "0x0"
	}
}
```

- eth_getTransactionReceipt
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data  '{"jsonrpc":"2.0","method":"eth_getTransactionReceipt","params":["0x5c26f679798c5ab5badb25f556aa6be5e7e2c8f4cf11e7cc96718cab8d787a8e"],"id":1}'

{
	"jsonrpc": "2.0",
	"id": 1,
	"result": {
		"blockHash": "0x80f52b3bf835875d38c17e299ab46ddad86a833b47769c18b1e14c0b6daa9237",
		"blockNumber": "0x8fc61d",
		"contractAddress": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
		"cumulativeGasUsed": "0x0",
		"from": "0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f",
		"gasUsed": "0x5498",
		"logs": [],
		"logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
		"root": "0x0000000000000000000000000000000000000000000000000000000000000000",
		"to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
		"transactionHash": "0x5c26f679798c5ab5badb25f556aa6be5e7e2c8f4cf11e7cc96718cab8d787a8e",
		"transactionIndex": "0x0",
		"type": "0x0"
	}
}
```
- eth_getUncleByBlockHashAndIndex 未实现
```
```

- eth_getUncleByBlockNumberAndIndex 未实现
```
```

### 智能合约编译器

- eth_getCompilers 未实现
```
```

- eth_compileSolidity 未实现
```
```

- eth_compileLLL 未实现
```
```

- eth_compileSerpent
```
```

### Filter类
- eth_newFilter https://eth.wiki/json-rpc/API#eth_newfilter
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_newFilter","params":[],"id":73}'

```

- eth_newBlockFilter
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_newBlockFilter","params":[],"id":73}'

{"jsonrpc":"2.0","id":73,"result":"0x42d45a91bbbd6e55b25871d079c8633b"}
```

- eth_newPendingTransactionFilter
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_newPendingTransactionFilter","params":[],"id":73}'

{"jsonrpc":"2.0","id":73,"result":"0x71fbc150acffacc510acc5415da60f29"}
```

- eth_uninstallFilter
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_uninstallFilter","params":["0xeabc5ca1d427f80061a526cf510b63e"],"id":73}'
```

- eth_getFilterChanges
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_getFilterChanges","params":["0xeabc5ca1d427f80061a526cf510b63e"],"id":74}'
```

- eth_getFilterLogs
  要求filter必须是log类的filter，Block和Tx的filter不适用，因此只能使用eth_newFilter创建。
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_getFilterLogs","params":["0xeabc5ca1d427f80061a526cf510b63e"],"id":74}'
```

- eth_getLogs
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"jsonrpc":"2.0","method":"eth_getLogs","params":[{"topics":["0x000000000000000000000000a94f5374fce5edbc8e2a8697c15331677e6ebf0b"]}],"id":74}'

```

### ethash
- eth_getWork 未支持
```
```
- eth_submitWork 未支持
```
```
- eth_submitHashrate 未支持
```
```

### db类
DB操作不影响stateDB
- db_putString 未支持
```
```
- db_getString 未支持
```
```
- db_putHex 未支持
```
```
- db_getHex 未支持
```
```

### personal类
- personal_deriveAccount
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data "{\"method\":\"personal_deriveAccount\",\"params\":[\"keystore:\/\/\/app\/mondo\/blockchain\/keystore\/UTC--2021-06-11T06-57-36.499816000Z--0f508f143e77b39f8e20dd9d2c1e515f0f527d9f\",\"m/44'/60'/0'/0/0\",true],\"id\":1,\"jsonrpc\":\"2.0\"}"

{"jsonrpc":"2.0","id":1,"error":{"code":-32000,"message":"not supported"}}
```

- personal_ecRecover
```
curl -X POST --data '{"jsonrpc":"2.0","method":"personal_ecRecover","params":["0xdeadbeaf", "0xf9ff74c86aefeb5f6019d77280bbb44fb695b4d45cfe97e6eed7acd62905f4a85034d5c68ed25a2e7a8eeb9baf1b8401e4f865d92ec48c1763bf649e354d900b1c"],"id":1}' -H "Content-Type: application/json" http://localhost:8545

{"jsonrpc":"2.0","id":1,"result":"0x3b7252d007059ffc82d16d022da3cbf9992d2f70"}
```

- personal_importRawKey
```
curl -X POST --data '{"jsonrpc":"2.0","method":"personal_importRawKey","params":["df937d2394ced72289f5c54646bd2fdde3b8548b166636f2a929cf83f014fddb", "the key is this"],"id":1}' -H "Content-Type: application/json" http://localhost:8545

{"jsonrpc":"2.0","id":1,"result":"0x6ab0a7b8b5c7a089f2c6137083c970c307147c10"}
```

- personal_initializeWallet
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"method":"personal_initializeWallet","params":["http://wolot.io"],"id":1,"jsonrpc":"2.0"}'

{"jsonrpc":"2.0","id":1,"error":{"code":-32000,"message":"unknown wallet"}}
```

- personal_listAccounts
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"method":"personal_listAccounts","params":[],"id":1,"jsonrpc":"2.0"}'

{"jsonrpc":"2.0","id":1,"result":["0xb7ff5eee043afc5e27b4ff05c3a6bed5cd3b978d","0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f"]}
```

- personal_listWallets
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"method":"personal_listWallets","params":[],"id":1,"jsonrpc":"2.0"}' 

{
	"jsonrpc": "2.0",
	"id": 1,
	"result": [{
		"url": "keystore://D:\\code\\git.wolot.io\\mondo\\blockchain\\cmd\\keystore\\UTC--2021-05-28T07-47-44.670529700Z--b7ff5eee043afc5e27b4ff05c3a6bed5cd3b978d",
		"status": "Locked",
		"accounts": [{
			"address": "0xb7ff5eee043afc5e27b4ff05c3a6bed5cd3b978d",
			"url": "keystore://D:\\code\\git.wolot.io\\mondo\\blockchain\\cmd\\keystore\\UTC--2021-05-28T07-47-44.670529700Zb7ff5eee043afc5e27b4ff05c3a6bed5cd3b978d"
		}]
	}, {
		"url": "keystore://D:\\code\\git.wolot.io\\mondo\\blockchain\\cmd\\keystore\\UTC--2021-05-28T07-49-11.055538600Z--0f508f143e77b39f8e20dd9d2c1e515f0f527d9f",
		"status": "Unlocked",
		"accounts": [{
			"address": "0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f",
			"url": "keystore://D:\\code\\git.wolot.io\\mondo\\blockchain\\cmd\keystore\UTC--2021-05-28T07-49-11.055538600Z--0f508f143e77b39f8e20dd9d2c1e515f0f527d9f"
		}]
	}]
}
```

- personal_lockAccount
```
 curl -X POST --data '{"jsonrpc":"2.0","method":"personal_lockAccount","params":["0x0f54f47bf9b8e317b214ccd6a7c3e38b893cd7f0"],"id":1}' -H "Content-Type: application/json" http://localhost:8545

{"jsonrpc":"2.0","id":1,"result":true}
```

- personal_newAccount
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"method":"personal_newAccount","params":["00000000"],"id":1,"jsonrpc":"2.0"}'

{"jsonrpc":"2.0","id":1,"result":"0xc20e48f794ff219c1e75743081a196a655c7c6e8"}
```

- personal_openWallet ETH KEYSTORE也还未实现这个方法
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"method":"personal_openWallet","params":["keystore://D:\\code\\git.wolot.io\\mondo\\blockchain\\cmd\\keystore\\UTC--2021-05-28T07-47-44.670529700Z--b7ff5eee043afc5e27b4ff05c3a6bed5cd3b978d","00000000"],"id":1,"jsonrpc":"2.0"}'

{"jsonrpc":"2.0","id":1,"result":null}
```

- personal_sendTransaction
```
curl -X POST --data '{"jsonrpc":"2.0","method":"personal_sendTransaction","params":[{"from":"0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f","to":"0xddd64b4712f7c8f1ace3c145c950339eddaf221d", "value":"0x1"},"00000000"],"id":1}' -H "Content-Type: application/json" http://localhost:8545

{"jsonrpc":"2.0","id":1,"result":"0x28f5737b9d268471a65e52ba47cc90e4cd542c38b30f28a4698573eabee58c74"}
```

- personal_sign
```
curl -X POST --data '{"jsonrpc":"2.0","method":"personal_sign","params":["0xdeadbeaf", "0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f", "00000000"],"id":1}' -H "Content-Type: application/json" http://localhost:8545

{"jsonrpc":"2.0","id":1,"result":"0x2a61d3ad6cee5e083838bdef6c7ea4ff447727055b81da63001df7150d632ccb26697237f5a03a51306a0563572551c078af7d979665c67ac63d6ba3a810cc501c"}
```

- personal_signAndSendTransaction
```

```
- personal_signTransaction
```

```

- personal_unlockAccount
```
curl -X POST -H "Content-Type:application/json" http://localhost:8545 --data '{"method":"personal_unlockAccount","params":["0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f","00000000",null],"id":1,"jsonrpc":"2.0"}'

{"jsonrpc":"2.0","id":1,"result":true}
```

- personal_unpair
```
```