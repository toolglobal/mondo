# 外部节点升级、部署指南

- 参数

|    参数名称    |                   参数值                    | 备注 |
| ------------- | ------------------------------------------ | ---- |
| ParamContract | 0xFe04B392AF295A18a17e3b43eD6d23EC7245501D |      |
| INITHEIGHT    | N/A                                        |      |
| CHAINID       | 8723                                       |      |

- 创世文件 genesis.json
```
{
  "genesis_time": "2018-08-27T00:00:00.000000000Z",
  "chain_id": "MondoV5-8723",
  "initial_height": "$INITHEIGHT",
  "consensus_params": {
    "block": {
      "max_bytes": "22020096",
      "max_gas": "-1",
      "time_iota_ms": "1000"
    },
    "evidence": {
      "max_age_num_blocks": "100000",
      "max_age_duration": "172800000000000",
      "max_bytes": "1048576"
    },
    "validator": {
      "pub_key_types": [
        "ed25519"
      ]
    },
    "version": {}
  },
  "validators": [
    {
      "address": "0BA034E7C5D4B99323427CE5FEF30FAAFCB78F02",
      "pub_key": {
        "type": "tendermint/PubKeyEd25519",
        "value": "TKauEYAucxigsuUP76NgQF0gZ41+eUdxcf396jxGmqY="
      },
      "power": "10",
      "name": ""
    },
    {
      "address": "AB4445F1E160A83A85990324E3F64A76E2A098FA",
      "pub_key": {
        "type": "tendermint/PubKeyEd25519",
        "value": "rtwTFfyO5swme14VfHIVHDd8veqUGABbpEUC68Hu6Hc="
      },
      "power": "10",
      "name": ""
    },
    {
      "address": "679C0E161B0326DA71C332115F9EC98AF97FF63C",
      "pub_key": {
        "type": "tendermint/PubKeyEd25519",
        "value": "Ym11X2yljTv26bnOPgzjvuZiuSxR+CcOvmfRh5qQtAI="
      },
      "power": "10",
      "name": ""
    },
    {
      "address": "FD884C1BB5F04669687F3062A2B2E0C58A1B24AC",
      "pub_key": {
        "type": "tendermint/PubKeyEd25519",
        "value": "Pum8PQQFUQCX0V2sfQ9uSTo336hHGE565TwJ/O8cefs="
      },
      "power": "10",
      "name": ""
    }
  ],
  "app_hash": ""
}
```
## 全新部署
适用于新部署节点和非共识节点（以前未参与TBP计划）的节点升级。
- 停止mondo程序
- 下载程序到/app/mondo/blockchain中
- 初始化底层配置 `./mondod --home=.mondo init`
- 初始化应用配置 `./mondod --home=.mondo app init`，修改ParamContract为 $ParamContract
- 覆盖.mondo/config/genesis.json
- 导入statedb `./mondod --home=.mondo app state import genesis_state.v5.json`
- 修改.mondo/config/config.toml
```toml
p2p.persistent_peers = "882d546b78fd5969de05ce324db7ed175bd6077d@18.139.250.111:26656,5d4a27ddd0e47f3814543c38048758d62a03931f@18.140.180.203:26656,24984b84b6e07f8eb1b8d207a146b1220ba229c1@13.228.188.50:26656,9c7b698a22c4652d7a277e54a22d53f261bc76cf@18.138.87.101:26656"
consensus.create_empty_blocks_interval = 60s
```
- 防火墙打开tcp 26656端口
- 启动 `nohup ./mondod --home=.mondo node &`，查询出块情况`tail -f nohup.out`

## 升级部署
适用于已部署节点升级，已部署节点但未参与TBP计划也可以采用本方法
- 停止mondo程序
- 下载程序，更新mondo为mondod
- 清除旧数据:`./mondod --home=.mondo unsafe_reset_all`
- 删除无用日志和文件，log目录和nohup.out
- 初始化应用配置 `./mondod --home=.mondo app init`，修改ParamContract为 $ParamContract
- 替换.mondo/config/genesis.json
- 导入statedb `./mondod --home=.mondo app state import genesis_state.v5.json`
- 启动 `nohup ./mondod --home=.mondo node &`，查询出块情况`tail -f nohup.out`

## 部署、升级API程序[可选]
API程序解析区块数据生成可视化的区块、交易、转账记录，并使用sqlite保存，方便查询，此功能为可选。最新的mondod提供兼容eth的web3 provider JSON RPC，API程序不再维护。

- 替换api程序 https://github.com/toolglobal/api/releases/download/v1.4.0/build.tar.gz
- 修改config.toml配置

```
bind = ":8889" # 监听8889 http端口
rpc = "127.0.0.1:26657" # 连接本地mondod节点的26657 tendermint rpc端口
dev = true # 开发模式
metrics = true # prometheus 监控
chainId = "8723" # 链id，mainnet：8723 testnet：8724
versions = [3] # 解析协议版本
startHeight = $INITHEIGHT # 开始解析区块高度 $INITHEIGHT
tgsBaseURL = "https://services.wolot.io" # 获取官方代币配置的接口

[limiter] # 合约查询限流，合约查询需要执行evm，性能损耗大，可能影响节点稳定
interval = "0h0m1s"
capacity = 100
```

- 启动即可

