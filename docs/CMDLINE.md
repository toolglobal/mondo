# mondo 命令行

[TOC]

## 命令行介绍
### usage
mondo 基于tendermint构建，默认支持tendermint所有命令，执行`./mondod -h`可查看指令帮助。

```
$ ./mondod -h
BFT state machine replication for applications in any programming languages

Usage:
  tendermint [command]

Available Commands:
  account                     Manage accounts
  app                         app sub-commands
  debug                       A utility to kill or watch a Tendermint process while aggregating debugging data
  gen-node-key                Generate a node key for this node and print its ID
  gen-validator               Generate new validator keypair
  help                        Help about any command
  init                        Initialize Tendermint
  light                       Run a light client proxy server, verifying Tendermint rpc
  probe-upnp                  Test UPnP functionality
  replay                      Replay messages from WAL
  replay-console              Replay messages from WAL in a console
  show-node-id                Show this node's ID
  show-validator              Show this node's validator info
  start                       Run the tendermint node
  testnet                     Initialize files for a Tendermint testnet
  unsafe-reset-all            (unsafe) Remove all the data and WAL, reset this node's validator to genesis state
  unsafe-reset-priv-validator (unsafe) Reset this node's validator to genesis state
  version                     Show version info
  wallet                      Manage Ethereum presale wallets

Flags:
  -h, --help               help for tendermint
      --home string        directory for config and data (default "C:\\Users\\axe\\.mondo")
      --log_level string   log level (default "info")
      --trace              print out full stack trace on errors

Use "tendermint [command] --help" for more information about a command.
```

其中`app` 子命令为mondo应用扩展的命令，使用`./mondod app -h`查看 app子命令帮助。

```
[root@localhost cmd]# ./mondod app -h
app sub-commands

Usage:
  tendermint app [command]

Available Commands:
  init        init app.toml
  state       state sub-commands
  tbp         TBP sub-commands
  version     Show version info

Flags:
  -h, --help   help for app

Global Flags:
      --home string        directory for config and data (default "/root/.mondo")
      --log_level string   log level (default "info")
      --trace              print out full stack trace on errors

Use "tendermint app [command] --help" for more information about a command.
```

- init 初始化应用配置文件
- state 状态树管理
- tbp TBP节点相关
- version 查看应用版本

### 账户管理（托管钱包管理）
 提供与以太坊一致的账户管理功能，可将账户托管在节点本地，请妥善保管和备份账户信息，防止丢失。
####  创建账户
```
./mondod --home=home account new # 输入密码后，将新建一个账户托管在本地
Your new account is locked with a password. Please give a password. Do not forget this password.
Password:
Repeat password:

Your new key was generated

Public address of the key:   0x8d2E730C3eB149dF47736F37aB6a744601125ff5
Path of the secret key file: ...\keystore\UTC--2021-07-05T05-57-36.449736800Z--8d2e730c3eb149df47736f37ab6a744601125ff5

```

#### 导入账户
```
./mondod --home=home account import keyfile # 通过私钥导入账户，keyfile中是账户私钥
```

#### 更新账户密码
```
./mondod --home=home account update 0x8d2E730C3eB149dF47736F37aB6a744601125ff5 # 更新0x8d2E730C3eB149dF47736F37aB6a744601125ff5的密码
```

#### 列出本地托管的账户
```
$ ./mondod --home=home account list
Account #0: {8d2e730c3eb149df47736f37ab6a744601125ff5} keystore://...\keystore\UTC--2021-07-05T05-57-36.449736800Z--8d2e730c3eb149df47736f37ab6a744601125ff5
```

### TBP子命令
节点加入节点竞选，成为共识节点，参与区块共识获取矿工费奖励和额外出矿奖励。TBP子命令均通过web3 RPC访问链，遵循web3 RPC原则。
```
$ ./mondod --home=home app tbp
TBP sub-commands

Usage:
  tendermint app tbp [command]

Available Commands:
  info        Show TBP information
  join        Join TBP plan with owner,the owner will be the operator of TBP
  setowner    Set new owner,the from must be the old owner
  withdraw    Withdrawn amount,the from must be the owner
```

#### 查看TBP节点信息
```
$ ./mondod --home=home app tbp info --web3=http://127.0.0.1:8545 --from=0x8d2e730c3eb149df47736f37ab6a744601125ff5
TBP address:D63D14331B012D2E4A7CA104D56A9B13FDF5B8EF PubKey:PubKeyEd25519{45C517B6BE3C6B128647EA2CB520667F99B7D0BFA743B51154B8F260FE310F7D} in 'config/priv_validator_key.json'
TBP Consensus Power:10 Owner:0x0F508F143E77b39F8e20DD9d2C1e515f0f527D9F Eraned:0 Status:OK
Latest round, Height:0, TokenStaked:0, NFTStaked:0, Earned:0

- Consensus Power 共识节点具有>0的共识power
- owner join时设置
- earned 节点收益，包括矿工费和DPos收益
- status TBP状态
- height：上一轮DPos高度
- tokenStaked：上一轮节点下所有验证者质押资产总和
- NFTStaked：上一轮节点下所有验证者登记NFT总和
- earned：上一轮节点收益
```

#### 加入节点竞选  
```
$  ./mondod --home=home app tbp join 0x8d2e730c3eb149df47736f37ab6a744601125ff5 --web3=http://127.0.0.1:8545 --from=0x8d2e730c3eb149df47736f37ab6a744601125ff5
TBP address:D63D14331B012D2E4A7CA104D56A9B13FDF5B8EF PubKey:PubKeyEd25519{45C517B6BE3C6B128647EA2CB520667F99B7D0BFA743B51154B8F260FE310F7D} in 'config/priv_validator_key.json'

Join success,hash:0x27738e8554f711953e8a6562f35690d17dffc56a6818b4cb4d7d77f1c95f7864

- 此命令将发送一笔交易，交易签名者为from，需要from账户有足够资产作为矿工费，from账户是托管在本地的账户
- 此命令将节点加入TBP节点竞选合约，节点信息在config/priv_validator_key.json中，本例中节点地址为A62D0D88351ECFD2F1DDE5469068BCBA8C113A9D
- 参数0x8d2e730c3eb149df47736f37ab6a744601125ff5将被指定为节点owner，对节点后续操作都需要owner权限，务必不能丢失owner私钥，否则将失去对节点的管理权限
- web3 指定节点的RPC地址，默认为http://127.0.0.1:8545
```
from账户需先解锁
```
curl -X POST -H "Content-Type:application/json" http://127.0.0.1:8545 --data '{"method":"personal_unlockAccount","params":["0x8d2e730c3eb149df47736f37ab6a744601125ff5","password",null],"id":1,"jsonrpc":"2.0"}'
```

#### 设置owner
```
$ ./mondod --home=home app tbp setowner 0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f --web3=http://127.0.0.1:8545 --from=0x8d2e730c3eb149df47736f37ab6a744601125ff5

TBP address:D63D14331B012D2E4A7CA104D56A9B13FDF5B8EF PubKey:PubKeyEd25519{45C517B6BE3C6B128647EA2CB520667F99B7D0BFA743B51154B8F260FE310F7D} in 'config/priv_validator_key.json'
SetOwner success,hash:0x69324671a2b166c038eabe0facf73333a800b1c4a22cbacf23d9c615de7cf6d8

- 此命令将发送一笔交易，交易签名者为from，需要from账户有足够资产作为矿工费，from账户是托管在本地的账户
- 设置0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f为新的owner
- from必须为旧的owner
```

#### 提取收益
```
$ ./mondod --home=home app tbp withdraw 0x678fc26dfb6447a6bcf370b52fe4117654b85233 100000000 --web3=http://127.0.0.1:8545 --from=0x0f508f143e77b39f8e20dd9d2c1e515f0f527d9f

TBP address:D63D14331B012D2E4A7CA104D56A9B13FDF5B8EF PubKey:PubKeyEd25519{45C517B6BE3C6B128647EA2CB520667F99B7D0BFA743B51154B8F260FE310F7D} in 'config/priv_validator_key.json'
Withdraw success,hash:0xb1794da6efc232127312dfd94817203398c9fc15234a1bcd87e473c7809b5eda

- 此命令将发送一笔交易，交易签名者为from，需要from账户有足够资产作为矿工费，from账户是托管在本地的账户
- 提取收益到账户0x678fc26dfb6447a6bcf370b52fe4117654b85233，金额为100000000(1.0 OLO) 
- from 为owner
```



