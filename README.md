# mondo 全节点操作手册
[TOC]

## 命令行介绍
### usage
```
[root@localhost blockchain]# ./mondo -h
mondo blockchain built with Tendermint

Usage:
  mondo [command]

Available Commands:
  balance     Query balance of node account
  collect     collect profit
  help        Help about any command
  init        Initialize mondo
  mortgage    Mortgage share
  node        Run the mondo node
  query       Query node info
  redeem      Redeem share
  version     Show version info
  voters      Query node voters
  withdraw    Withdraw value from node account to wallet

Flags:
  -h, --help          help for mondo
      --home string   directory for config and data (default "/root/.mondo")
      --trace         print out full stack trace on errors
```

- balance 查询节点账户余额
- collect 归集节点收益（DPOS收益和交易手续费）
- help 帮助
- init 初始化节点配置文件
- mortgage 抵押资产参与DPOS机制
- node 执行全节点
- query 查询节点信息
- redeem 赎回已抵押资产
- version 查询版本信息
- voters 查询投票给本节点的用户
- withdraw 将节点收益提现到普通钱包账户

### 查询节点账户余额
```
[root@localhost cmd]# ./mondo --home=.mondo balance
code 5, log Not Found address
ERROR: code 5, log Not Found address

如果节点账户未上链会出错，可以通过普通钱包给节点账户转账的方式创建节点账户。节点账户地址为：$home/config/priv_validator_key.json中address

[root@localhost blockchain]# ./mondo --home=.mondo balance
address: 2E160A40FD6E6FB356CEFB23EDF0E64F34E7BA39  balance: 4000999937000
```

###  抵押 

抵押10000 OLO，返回交易hash；抵押会从节点账户扣除手续费21000，抵押后节点账户余额减少。抵押生效高度为下一个DPOS高度。
```
[root@localhost blockchain]# ./mondo --home=.mondo mortgage 1000000000000
mortgage success tx: 0xcf46b73da1d10ff5658b1fe8f02ea09cbee5c85ecde0d4273f8c837e1a128e49
```
### 查询节点信息
```
[root@localhost blockchain]# ./mondo --home=.mondo query
{
    "address": "D9837D1C31CD819B701B54E80444AAF8F469F72F",//节点地址
    "nonce": 5,//nonce
    "power": 10,//投票权
    "genesis": true,//是否是创世节点
    "runFor": true,//是否参与超级节点投票
    "balance": "5320483373",//累积收益余额
    "mortgaged": "2000000000000",//已抵押资产
    "toMortgage": "0",//待抵押资产
    "redeem": false,//是否赎回
    "voted": "100000"//用户总投票数
}
```

###  查询投票给本节点的用户列表
```
[root@localhost blockchain]# ./mondo --home=.mondo voters
{
    "address": "D9837D1C31CD819B701B54E80444AAF8F469F72F",
    "voted": "3000",
    "voters": [
        {
            "address": "0x0aD29A24DD422e99dC2D63E8B8eA44EdCa28F068",
            "amount": "1000"
        },
        {
            "address": "0x0C79497Fda53761cf94276330251CE50DC8659B8",
            "amount": "1000"
        },
        {
            "address": "0x0c93FA2c9Ff36836c5d66061c43aa3aFF185326b",
            "amount": "1000"
        }
     ]
}
```
### 赎回
```
[root@localhost blockchain]# ./mondo --home=.mondo redeem
redeem success tx: 0x64105b0c9690601aec3bb1f190216e781f1d6b98bf6dc491329c249ff251a1d8
赎回会从节点账户扣除手续费21000，生效高度为下一轮DPOS高度。
```

### 获取收益
```
将节点累积所得收益转存到节点账户，获取收益会从节点账户扣除手续费21000。

[root@localhost blockchain]# ./mondo --home=.mondo balance  # 节点账户当前余额
address: D9837D1C31CD819B701B54E80444AAF8F469F72F  balance: 8000999937000
[root@localhost blockchain]# ./mondo --home=.mondo query #节点收益累积余额
{
    "address": "D9837D1C31CD819B701B54E80444AAF8F469F72F",
    "nonce": 6,
    "power": 10,
    "genesis": true,
    "runFor": true,
    "balance": "5846950655",
    "mortgaged": "2000000000000",
    "toMortgage": "0",
    "redeem": true,
    "voted": "100000"
}
[root@localhost blockchain]# ./mondo --home=.mondo collect # 获取收益
collect success tx: 0x76485163a495d29b4a823a210a65e3df4bd2135cd04bb77b684bc2c20f651191
[root@localhost blockchain]# ./mondo --home=.mondo query # 获取收益后，累积收益归0
{
    "address": "D9837D1C31CD819B701B54E80444AAF8F469F72F",
    "nonce": 7,
    "power": 10,
    "genesis": true,
    "runFor": true,
    "balance": "0",
    "mortgaged": "2000000000000",
    "toMortgage": "0",
    "redeem": true,
    "voted": "100000"
}
[root@localhost blockchain]# ./mondo --home=.mondo balance # 获取收益后，节点账户余额增加
address: D9837D1C31CD819B701B54E80444AAF8F469F72F  balance: 8006847916655
```

### 提现
```
将节点账户资产提现到普通钱包，会从节点账户扣除手续费21000。
[root@localhost blockchain]# ./mondo --home=.mondo balance # 提现前节点余额
address: 2E160A40FD6E6FB356CEFB23EDF0E64F34E7BA39  balance: 5000999958000
[root@localhost blockchain]# ./mondo --home=.mondo withdraw 0x0F508F143E77b39F8e20DD9d2C1e515f0f527D9F 1000000000000 # 提现10000 OLO到0x0F508F143E77b39F8e20DD9d2C1e515f0f527D9F
withdraw success tx: 0xf2d01dc8d4bfbbb6b0de756f16df38be2f39018e6827863d244942752e7a3612
[root@localhost blockchain]# ./mondo --home=.mondo balance # 提现后余额
address: 2E160A40FD6E6FB356CEFB23EDF0E64F34E7BA39  balance: 4000999937000
```

## 加入mondo网络
### 目录结构
```
[root@localhost .mondo]# pwd
/root/.mondo
[root@localhost .mondo]# tree -C -L 2
.
├── config
│   ├── addrbook.json
│   ├── config.toml
│   ├── genesis.json
│   ├── node_key.json
│   └── priv_validator_key.json
└── data
    ├── blockstore.db
    ├── chaindata.db
    ├── cs.wal
    ├── dpos.db
    ├── evidence.db
    ├── mondo_dpos.db
    ├── priv_validator_state.json
    ├── state.db
    └── tx_index.db
```
如上图所示，config是配置文件目录，data是数据目录。
- genesis.json 创世文件
- config.toml 节点配置文件
- priv_validator_key.json 节点配置文件

### 部署节点
- 初始化配置文件 `./mondo --home=.mondo init`
  会在.mondo目录下生成默认的配置文件数据目录
- 替换创世文件
从OLO联盟获取mondo链的创世文件genesis.json，并覆盖本地的genesis.json。
- 修改P2P，连接到mondo网络
修改config.toml中seeds项，填写节点要连接的其他节点。如：
```
seeds = "D9837D1C31CD819B701B54E80444AAF8F469F72F@192.168.8.123:26656,A8435DD54DA88322F0122A13FF429A9FAF9AA859@192.168.8.125:26656,2E160A40FD6E6FB356CEFB23EDF0E64F34E7BA39@192.168.8.142:26656,ACF92FEE80744C2B9DC1677EDBE695A80F4E18EE@192.168.8.143:26656"
```
- 启动节点
`nohup ./mondo --home=.mondo node &`，检查nohup.out日志是否正常同步区块。输出“Committed state”表示正常同步区块。

### 竞选超级节点
- 首先节点需要实时同步区块，保持全节点数据最新
- 向数金链联盟提出申请
- 抵押OLO资产参与竞选
- 参与共识，获取收益
- 节点要求：提供节点公钥和地址，节点IP地址和P2P端口（对外开放），健康检测端口（默认tcp/26660），质押一定量OLO；节点需有较强的运维能力保证节点稳定，如果节点不稳定会被踢出。