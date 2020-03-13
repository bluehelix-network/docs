# 快速启动

由于测试网在快速迭代开发中，我们现在提供预编译好的可执行文件，请通过[官方渠道](https://github.com/bluehelix-network/testnet/blob/v0.1.1/v0.1.1)下载，目前测试网使用的软件版本为 v0.1.1。

测试网的跨链资产仅支持BTC测试网，以太坊Ropsten测试网，其中ERC20代币仅支持Ropsten测试网的合约地址（TODO: ERC20代币合约地址）。充入其他资产将无法找回，请谨慎操作。

## 启动币核链全节点

### 下载配置文件与创世文件
下载 [仓库](https://github.com/bluehelix-network/testnet/tree/v0.1.1/v0.1.1) 中的 config 目录到本地的 `$HOME/.bhchain` 目录下。在 `$HOME/.bhchain/config/config.toml` 配置文件中对节点的别名 `moniker` 进行编辑：  

```
# A custom human readable name for this node
moniker = "<your_custom_moniker>"
```

### 启动节点
#### 使用二进制程序启动
连入测试网需要在本地启动两个可执行程序：bhchain 和 chainnode。从[仓库](https://github.com/bluehelix-network/testnet/tree/v0.1.1/v0.1.1)中下载对应操作系统版本的可执行文件到本地。
  
[下载 chainnode 配置文件 config.yml](https://github.com/bluehelix-network/testnet/blob/v0.1.1/v0.1.1/chainnode/config.yml)，启动 chainnode:

```
./chainnode -c config.yml
```

启动 bhchain:

```
./bhchain start --home ~/.bhchain --chainnode-url 127.0.0.1:8888
```

#### 使用 docker 启动
[下载 docker-compose.yml](https://github.com/bluehelix-network/testnet/blob/v0.1.1/v0.1.1/docker-compose.yml)，

然后，执行命令

```
docker-compose -f docker-compose.yml up -d
```

成功后会在本地启动 bhchain 和 chainnode 两个容器并连接到测试网络。

## 与币核链进行交互

当全节点与全网同步所有区块后，我们可以用命令行工具(bhcli)与币核链进行交互，可以运行以下指令查询所有的命令。

```bash
$ bhcli help
```

我们给出跨链资产充币，转账和提币的流程简介，以以太坊Ropsten测试网为例。

### 1. 创建和管理币核链托管单元
```bash
$ bhcli keys add bhuser --home node/
```
通过该命令我们在指定的node目录下创建了一个bhuser的托管单元（创建过程中需要输入你的密码对托管单元密钥进行加密存储），创建成功后展示如下：
```
{
  "name": "bhuser",
  "type": "local",
  "address": "BHYPnVEFuEqyqG3cBk7ocKU3AGjEyQE26dg",
  "pubkey": "bhpub1addwnpepq2ukkkcvre327tqfhetts5happwl2jnwnanhfefeue9p4jdhx99jz9c726e"
}
```

### 2. 创建以太坊的跨链托管地址
```bash
$ bhcli tx keygen keygen  bhuser eth BHYPnVEFuEqyqG3cBk7ocKU3AGjEyQE26dg  --chain-id bhchain-testnet --home node/
```
通过这个命令我们为bhuser创建eth跨链托管单元地址，命令发送执行后等待2-3个区块后（密钥的分布式生成需要一定的时间），我们通过下面的命令查询对应的托管单元信息，可以获取到eth的跨链托管地址：
```
$ bhcli query cuinfo BHYPnVEFuEqyqG3cBk7ocKU3AGjEyQE26dg --chain-id bhchain-testnet --home node/
```
查询的结果展示为：
```
{
  "type": "bhchain/CustodianUnit",
  "value": {
    "cu_type": "1",
    "address": "BHYPnVEFuEqyqG3cBk7ocKU3AGjEyQE26dg",
    "public_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "AmvTia/5ovwaCg/nud5FTvXg0OJ727wfXWf3JIHwfbqr"
    },
    "sequence": "0",
    "coins": [ ],
    "coins_hold": [],
    "assets": [
      {
        {
        "denom": "eth",
        "address": "0x97efBEAd089c9B57C4d5ed4a57d4ebBE3659d34B",
        "enbale_sendtx": true
      }
    ],
    "asset_pubkey": "A/dbw3DsU9HGTnglann9ZvlGl1gCPsC+8/2gWNrjhcQ3",
  }
}
```
从查询到的信息看，我们为托管单元在创建了一个eth的跨链托管地址(0x97efBEAd089c9B57C4d5ed4a57d4ebBE3659d34B)，并且这个地址的密钥由各个记账人节点分布式保存其中的分片，公钥在托管单元上可见（assert_pubkey)。

### 3. 充入跨链资产
```bash
$ bhcli tx transfer deposit bhuser BHYPnVEFuEqyqG3cBk7ocKU3AGjEyQE26dg 0x97efBEAd089c9B57C4d5ed4a57d4ebBE3659d34B 200000000000000000eth 0xe9b435405af39c4d3d7363840f5e6604ec7c0a1ed5af122d4422fe391254936c 0 memo 7458322  --chain-id bhchain-testnet --home node/

```
在以太坊Ropsten测试网上，我们对刚才生成的跨链托管地址进行一次充值操作，转入0.2eth，交易发送成功后，我们通过该命令把对应的充值信息提交到bluehelix链上，bluehelix链校验通过后，会将该资产记录入对应的托管单元上，现在你可以开始对该资产进行转账或提现等相关操作。
### 4. 跨链资产转账
```bash
$ bhcli tx send bhuser  BHccpSzNbAPue6QBTfN8259t12CfxC9NY2K  100000000000000000eth --chain-id bhchain-testnet --home node/
```
通过该命令我们将当前的托管单元充值的0.2eth向另外一个托管地址转出了0.1eth，对方的账户会增加0.1eth的资产。
### 5. 提出跨链资产
```bash
bhcli tx transfer withdrawal BHccpSzNbAPue6QBTfN8259t12CfxC9NY2K 0xC933C741416151dAcFE9428d39222f747e2b45EB 79000000000000000eth 21000000000000000 --chain-id bhchain-testnet --home node/
```
通过该命令，托管用户(BHccpSzNbAPue6QBTfN8259t12CfxC9NY2K)把自己通过交易获取到的0.1eth(去除支付的手续费后还有0.079eth)提现到自己的eth账户(0xC933C741416151dAcFE9428d39222f747e2b45EB 非托管地址）上，通过一定区块高度后，用户可以在自己的账户看到提现到账信息。