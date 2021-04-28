# OLO链上发行ORC20代币指南

## 概述
OLO链采用与以太坊类似的evm虚拟机，支持solidity合约，所以以太坊的合约不用修改可以直接在OLO链上使用。

## OLO链相关开源资料
- API程序 https://github.com/wolot/api API文档说明（签名说明）https://github.com/wolot/api/blob/master/docs.md
- sdk（golang） https://github.com/wolot/gosdk
- sdk（java） https://github.com/wolot/javasdk
- 公共API地址（低频使用）：https://olo.ibdt.tech

## 合约操作说明
- 部署合约、调用：部署合约需要发起一笔交易，接口`/v2/contract/transactions`
- 合约查询：查询合约与调用合约类似，只是调用接口不同，不改变链数据，不消耗gas。接口:`/v2/contract/query`

## 合约操作实例
已部署ERC20合约以及对其调用发起转账等为例。

### 准备合约bytecode
- 使用solidity webIDE Remix http://remix.ethereum.org/
- 在remix中编译代码，设置部署参数，生成合约部署的bytecode

### 部署合约
- 调用/v2/contract/transactions接口，参数如下:
```
type SignedEvmTx struct {
	CreatedAt uint64 `json:"createdAt"` // 时间戳，可选
	GasLimit  uint64 `json:"gasLimit"`  // gas限额
	GasPrice  string `json:"gasPrice"`  // gas价格，最低为1
	Nonce     uint64 `json:"nonce"`     // 交易发起者nonce
	Sender    string `json:"sender"`    // 交易发起者公钥
	Body      struct {
		To    string `json:"to"`    // 交易接受者地址或合约地址，创建合约时为空
		Value string `json:"value"` // 交易金额
		Load  string `json:"load"`  // 合约负载，原生币OLO转账时为空
		Memo  string `json:"memo"`  // 备注 可为空
	} `json:"body"`
	Signature string `json:"signature"` // 交易签名
}
```
- 将步骤1生成的合约bytecode放到load中，value通常为0，To为空，设置足够的gasLimit，发送上链即可
- 合约地址：和以太坊一样的生成方式 `contractAddr := crypto.CreateAddress(ethcmn.HexToAddress(tx.Sender.ToAddress().Hex()), nonce).Hex()`

### 转账
与合约部署类型，To改为代币合约地址，load改为转账的bytescode；load如下生成：
```
	abiIns, err := abi.JSON(strings.NewReader(`[{"constant":false,"inputs":[{"name":"_to","type":"address"},{"name":"_value","type":"uint256"}],
	"name":"transfer","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"}]`))
	loadbytes, err := abiIns.Pack("transfer", _to, _value)
```

### 查询代币余额
与转账类型，请求的url修改为:/v2/contract/query，load如下生成:
```
	abiIns, err := abi.JSON(strings.NewReader(`[{"constant":true,"inputs":[{"name":"_owner","type":"address"}],"name":"balanceOf",
	"outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"}]`))
	bin, err := abiIns.Pack("balanceOf", common.HexToAddress(address))
```
接口返回的ret需要按照`balanceof`方法ABI进行解析。

### gosdk说明
gosdk里有合约的操作方法
- 部署合约 DeployTx
- 调用合约 InvokeTx
- 查询合约 QueryTx