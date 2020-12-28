## 下载程序
```
链核心：https://olo.ibdt.tech/docs/blockchain.tgz
API(不含历史交易记录)：https://olo.ibdt.tech/docs/api_little.tgz 40MB
```

## 全新部署
- 解压blockchain.tgz到/app/mondo/blockchain目录
- 重新初始化 `./mondo --home=.mondo init`
- 拷贝genesis.json/genesis_xstate.json/genesis_minepool.json/genesis_params.json移动到.mondo/config目录,覆盖
- 导入历史数据：./mondo --home=.mondo app import --state=state --file=genesis_state.json
- 修改改配置文件config/config.toml
```
p2p.persistent_peers = "882d546b78fd5969de05ce324db7ed175bd6077d@18.139.250.111:26656,5d4a27ddd0e47f3814543c38048758d62a03931f@18.140.180.203:26656,24984b84b6e07f8eb1b8d207a146b1220ba229c1@13.228.188.50:26656,9c7b698a22c4652d7a277e54a22d53f261bc76cf@18.138.87.101:26656"
consensus.create_empty_blocks_interval = 60s
```
- 启动链核心：nohup ./mondo --home=.mondo node &
- tail -f nohup.out 查看区块同步情况

## 部署API程序
- 解压api_little.tgz到/app/mondo/api
- 【可选】修改配置文件BDE合约地址为:0xdfaEEc846218cD93A877152061F1ff6287E22548
- 执行nohup ./api &
