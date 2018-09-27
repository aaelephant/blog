* 创建数据目录tmpPrivate

		mkdir tmpPrivate
    
* 创建初始化json文件

		touch genesis.json
		
* genesis.json内容

		{
  		"config": {
        "chainId": 1,
        "homesteadBlock": 0,
        "eip155Block": 0,
        "eip158Block": 0
    		},
  		"alloc"      : {},
  		"coinbase"   : 		"0x0000000000000000000000000000000000000000",
  		"difficulty" : "0x20000",
  		"extraData"  : "",
  		"gasLimit"   : "0x2fefd8",
  		"nonce"      : "0x0000000000000042",
  		"mixhash"    : "0x0000000000000000000000000000000000000000000000000000000000000000",
  		"parentHash" : "0x0000000000000000000000000000000000000000000000000000000000000000",
  		"timestamp"  : "0x00"
		}
		
* 创世区块

		geth --datadir "./" init genesis.json
		
* 创建私有链条

		sudo geth –rpc –rpcport "8078" –rpccorsdomain '*' –datadir="data dir" –port 30309 –nodiscover –rpcapi 'db,eth,net,web3,debug' –networkid 1006 console 2>>geth.log /*nodiscover 不被其它节点发现*/
		targetgaslimit 每个块的gas上限，这里可以暂时理解为容量
		rpc –启动rpc通信，可以进行智能合约的部署和调试
		rpcaddr –rpc接口的地址
		rpcport –rpc接口的端口号 
		port –网络监听端口，用于节点之间通信 
		rpcapi –设置rpc的范围，暂时开启eth,web3,personal足够 		networkid –设置当前区块链的网络ID，是一个数字，可以随便写 
		identity –区块链的标示，随便填写，用于标示目前网络的名字 		nodiscover 禁止被网络中其它节点发现，需要手动添加该节点到网络 
		maxpeers 最大节点数量 
		datadir –设置当前区块链网络数据存放的位置 
		unlock –解锁某用户（此处用用户坐标来控制，解锁后的用户调用接口发起交易时，不要需要提供密码） 
		rpccorsdomain 限制rpc访问源的ip，代表不限制 mine 允许挖矿 
		console –启动命令行模式，可以在Geth中执行命令
		
* 基本命令

		eth.accounts --账户列表
		personal.newAccount("password") --创建账户
		miner.start() --挖矿
		miner.stop() --停止挖矿
		eth.accounts[0] --第0个账户
		eth.getBalance(eth.accounts[0]) --账户余额
		eth.sendTransaction(from:acc0,to:acc1,value:amount) --acc0账户转账给acc1账户amount个以太币,转账后要开启挖矿才能看到账户余额变化,因为要交易要写入区块中
		miner.setEtherbase(eth.accounts[1]) --更改coinbase账户
		txpool.status 查看交易池状态
		eth.getBlock("pending",true).transactions 查看pending状态的交易详细信息
		eth.getBlock(块数)
		
* 安装Mist

		curl https://install.meteor.com/ | sh
		npm install -g electron@1.3.13
		npm install -g gulp
		
		git clone https://github.com/ethereum/mist.git
		cd mist
		git submodule update --init
		npm install secp256k1 (yarn执行前installsecp256k1,yarn中的secp256地址有误)
		yarn
		yarn dev:electron --rpc /User/Tiger/tmpPrivate/geth.ipc --node-networkid 1234 --node-datadir /User/Tiger/tmpPrivate
		
		cd mist/interface
		meteor --no-release-check 启动Mist服务
		
		启动Mist界面
		yarn dev:electron --rpc http://localhost:8087
		