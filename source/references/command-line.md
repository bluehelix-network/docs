# 命令行参考

## status
查询链的状态

##### 示例
```
bhcli  status
```
##### 成功返回
```
{
  "node_info": {
    "protocol_version": {
      "p2p": "7",
      "block": "10",
      "app": "0"
    },
    "id": "b2db55fc78167a25ad85164ffa337156d2e9cc50",
    "listen_addr": "tcp://0.0.0.0:26656",
    "network": "bhchain-testnet",
    "version": "0.32.7",
    "channels": "402021222330380070",
    "moniker": "node0",
    "other": {
      "tx_index": "on",
      "rpc_address": "tcp://0.0.0.0:26657"
    }
  },
  "sync_info": {
    "latest_block_hash": "3B7AB98BB8EB8C159730553F7C8B96D20C35263A852D76CC0D76D52AC2EFCB19",
    "latest_app_hash": "48A621D1158D6B09FEA1C64BEDFEFF00577F313D71F4DBD7E65EF7B41CBB61D0",
    "latest_block_height": "9082",
    "latest_block_time": "2020-03-13T13:58:49.6930023Z",
    "catching_up": false
  },
  "validator_info": {
    "address": "FB86F30D56843CF0C9760C6D7C028FCE3C63409D",
    "pub_key": {
      "type": "tendermint/PubKeyEd25519",
      "value": "K4BrEuqGmEn14J4YKgR+SKWpgBKGivcqLBscWOE1aI0="
    },
    "voting_power": "100"
  }
}

```
## config
### 显示client 的配置

##### 示例
```
bhcli config
```
##### 成功返回
```
chain-id = "bhchain-testnet"
indent = true
output = "json"
trust-node = true
```

### 配置client
将bhclient 的常用的配置信息存放在.bhcli/config/config.toml中
```
bhcli config <key> [value] [flags]
```

##### 示例
```
bhcli config indent  false
bhcli config chain-id  bhchain-testnet
bhcli config output  text
bhcli config trust-node  true
```

## query

### tendermint-validator-set

查询当前validators
```
bhcli query tendermint-validator-set
```

#### 示例
```
bhcli query tendermint-validator-set
```
#### 成功返回
```
{
  "block_height": "283",
  "validators": [
    {
      "address": "bhvalcons14rs62gppmu89l0dgdnelvxua06cx4jqhrpjtqz",
      "pub_key": "bhvalconspub1zcjduepqu6luln9tr2pvapag4gg7lydreqmfw3f3jm0xx5hmwjq2x0mluy8qjczv5x",
      "proposer_priority": "-100",
      "voting_power": "100"
    },
    {
      "address": "bhvalcons1h0muy2683gyp6ra2qph9hxwdfmxzw6x4xtkm8m",
      "pub_key": "bhvalconspub1zcjduepq69plcv4nzg27qashf328q0p6uc8cdpl4u3fz5sd2ugz34nk0u4ws2zrp0f",
      "proposer_priority": "-100",
      "voting_power": "100"
    },
    {
      "address": "bhvalcons1uqdrc98tjanxmdp4pa0uv3hdwny30jl0u4j7qp",
      "pub_key": "bhvalconspub1zcjduepqr56er5xnqdtzwckfv2z6ju423zv2m9plhgc34rvq34y5rjc3xfws6e7yw5",
      "proposer_priority": "-100",
      "voting_power": "100"
    },
    {
      "address": "bhvalcons1lwr0xr2kss70pjtkp3khcq50ec7xxsyag9dg3r",
      "pub_key": "bhvalconspub1zcjduepq9wqxkyh2s6vyna0qncvz5pr7fzj6nqqjs690w23vrvw93cf4dzxsthasln",
      "proposer_priority": "300",
      "voting_power": "100"
    }
  ]
}

```


### block
查询指定高度的区块内容
#### 示例
```
bhcli query  block 100
```
#### 成功返回
```
{
  "block_meta": {
    "block_id": {
      "hash": "725AF85D2379A81D413B9A5CFA9A58F5524B13CCC07658043459B1693614761A",
      "parts": {
        "total": "1",
        "hash": "0DA561F01BFBDBF0A434DBEB61B3CECFE2C8237EAC8FB6F865AF6B21879D8FF0"
      }
    },
    "header": {
      "version": {
        "block": "10",
        "app": "0"
      },
      "chain_id": "bhchain-testnet",
      "height": "100",
      "time": "2020-03-12T08:55:26.2535414Z",
      "num_txs": "1",
      "total_txs": "8",
      ....

}
```

### txs
#### 示例
```

```

#### 成功返回
```

```

### tx

根据hash查找交易 

```
bhcli query tx [hash]
```


#### 示例
```
bhcli query tx E81EC801B96C99E99BA2EAA73624AF5FAA7A0356894846BB11C70D57B62937AD --trust-node
```

#### 成功返回
```
{
  "height": "130",
  "txhash": "E81EC801B96C99E99BA2EAA73624AF5FAA7A0356894846BB11C70D57B62937AD",
  "data": "{Category:4 Flows:[{Symbol:eth CUAddress:1A44C7E097ECA1EFB9EAE78853A0B8EDD70A069D OrderID:efc5b260-e389-48f6-ae8d-197d60ba6ce6 OrderType:4 OrderStatus:7} {CuAddress:BHNHpBtP97HX4QCyPRbeH4K7LupNVwe9ViM Multisignedadress:0x9F0Bc5D2DAFa22a8D1A496476D9abF4A7e3C2090 Symbol:eth Index:0 Txhash:0x5496614bbea29b2e91a90a285f809e9960e64f4ebe7c9ce2dd7c6b3384c0618d Amount:10000000000000000 OrderID:efc5b260-e389-48f6-ae8d-197d60ba6ce6 DepositType:10 Memo:memo}]}",
  "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":[{\"type\":\"deposit\",\"attributes\":[{\"key\":\"sender\",\"value\":\"BHj2wujKtAxw9XZMA7zDDvjGqKjoYUdw1FZ\"},{\"key\":\"recipient\",\"value\":\"BHNHpBtP97HX4QCyPRbeH4K7LupNVwe9ViM\"},{\"key\":\"symbol\",\"value\":\"eth\"},{\"key\":\"hash\",\"value\":\"0x5496614bbea29b2e91a90a285f809e9960e64f4ebe7c9ce2dd7c6b3384c0618d\"},{\"key\":\"amount\",\"value\":\"10000000000000000\"},{\"key\":\"index\",\"value\":\"0\"},{\"key\":\"memo\",\"value\":\"memo\"}]},{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"deposit\"}]}]}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
....        
    }
```

### token
查询支持的币种信息
```bash
bhcli query token token tusdt 
```
返回值
```
{                                                           
  "symbol": "tusdt",                                        
  "token_info": {                                           
    "symbol": "tusdt",                                      
    "issuer": "0xC9476A4919a7E5c7e1760b68F945971769D5c1D8", 
    "chain": "eth",                                         
    "type": "2",                                            
    "is_send_enabled": true,                                
    "is_deposit_enabled": true,                             
    "is_withdrawal_enabled": true,                          
    "decimals": "6",                                        
    "total_supply": "30000000000000000",                    
    "collect_threshold": "200000000",                       
    "deposit_threshold": "200000000",                       
    "open_fee": "28000000000000000000",                     
    "sys_open_fee": "28000000000000000000",                 
    "withdrawal_fee": "8000000000000000",                   
    "max_op_cu_number": "10",                               
    "systransfer_amount": "800000000000000",                
    "op_cu_systransfer_amount": "100000000000000000",       
    "gas_limit": "80000",                                   
    "gas_price": "1000"                                     
    }  
}                                                       
```

### order
有些发送到链上的交易会产生order，比如keygen(创建资产地址)、deposit（充币）,withdrawal(提币)等交易。可以根据交易返回的orderid，查询order详情。
```bash
bhcli query order order 3b16978a-a435-4b64-acc3-7e15b571319b 
```
返回值
```
{
  "type": "bhchain/order/OrderKeyGen",
  "value": {
    "OrderBase": {
      "cu_address": "BHYTXFNFVrb8WPh5in7Lfz2JVgDyEWQ252V",
      "id": "3b16978a-a435-4b64-acc3-7e15b571319b",
      "order_type": "1",
      "symbol": "btc",
      "status": "10"
    },
    "key_nodes": [
      "BHMbeYCvT6wE3LM2fBcr6hhNExNLAyffzVP",
      "BHYTXFNFVrb8WPh5in7Lfz2JVgDyEWQ252V",
      "BHYVhhstYXg5Ke5zSGNMG6j6r6YiErmMWK3",
      "BHiJbAipJgJMdHKCZ2NFJoDCnZ8HaKUT34v"
    ],
    "sign_threshold": "3",
    "to": "BHaTpyRAQvg9fo2KDRzf4EwtjrVW3ZanJPs",
    "open_fee": [
      {
        "denom": "bht",
        "amount": "28000000000000000000"
      }
    ],
    "multi_sign_address": "mwW98DAVfoojM7fkn1RW871PdjBZh7qF6L"
  }
}
```

### Supply

#### 查询token发行数量
```
bhcli query supply total
```

##### 示例
```
bhcli query supply total
```

##### 成功返回
```
{
    "denom": "bht",
    "amount": "2000000673785078713210129395"
}
```

### mint
#### 查询mint的参数
```
bhcli query mint params
```
##### 示例 
```
bhcli query mint params
```

##### 成功返回
```
{
  "mint_denom": "bht",
  "blocks_per_year": "10519200",
  "inflation": "0.030000000000000000",
  "initial_price": "0.100000000000000000",
  "current_price": "0.100000000000000000",
  "node_cost_per_month": "2600.000000000000000000"
}
```
### gov 
#### 查询gov模块参数

##### 示例
```
bhcli query gov params
```
##### 成功返回
```
{
  "voting_params": {
    "voting_period": "172800000000000"
  },
  "tally_params": {
    "quorum": "0.334000000000000000",
    "threshold": "0.500000000000000000",
    "veto": "0.334000000000000000"
  },
  "deposit_params": {
    "min_init_deposit": [
      {
        "denom": "bht",
        "amount": "100000000000000000000000"
      }
    ],
    "min_deposit": [
      {
        "denom": "bht",
        "amount": "10000000000000000000000000"
      }
    ],
    "max_deposit_period": "172800000000000"
  }
}
```

#### 查询一个提案
根据proposal id精确的查询某个提案的内容
```
bhcli query gov proposal [proposal-id] [flags]
```
##### 参数说明

| 名称   | 类型   | 参数说明|
| ------ | ------ | ------ |
|proposal-id | string | proposal id|


##### 示例
```
bhcli query gov proposal 1
```
##### 成功返回
```
{
  "content": {
    "type": "cosmos-sdk/TextProposal",
    "value": {
      "title": "Test Proposal Title",
      "description": "Test Proposal Contents"
    }
  },
  "id": "1",
  "proposal_status": "DepositPeriod",
  "final_tally_result": {
    "yes": "0",
    "abstain": "0",
    "no": "0",
    "no_with_veto": "0"
  },
  "submit_time": "2020-03-12T15:19:32.4261328Z",
  "deposit_end_time": "2020-03-14T15:19:32.4261328Z",
  "total_deposit": [
    {
      "denom": "bht",
      "amount": "100000000000000000000000"
    }
  ],
  "voting_start_time": "0001-01-01T00:00:00Z",
  "voting_end_time": "0001-01-01T00:00:00Z"
}
```

#### 查询一类提案
```
bhcli query gov proposals  [flags]
```
##### 常用查询选项

| 名称  | 类型 | 参数说明 |
| ------ | ------ | ------ |
| --depositor| string | 查询depositor抵押了资产的提案 |
| --voter | string | voter 投过票的提案|
| --status | string | 提案目前的状态|



##### 示例
```
bhcli query gov proposals --depositor $(bhcli keys show -a alice)
bhcli query gov proposals --voter $(bhcli keys show -a alice)
bhcli query gov proposals --status (DepositPeriod|VotingPeriod|Passed|Rejected)
```

#### 查询某voter对某提案的抵押信息
```
bhcli query gov deposit [proposal-id] [depositer-addr] [flags]
```

##### 参数说明

| 名称 | 类型 | 参数说明 |
| ------ | ------ | ------ |
| proposal-id | string | proposal id |
| depositer-addr | string | depositer地址|

##### 示例
```
bhcli query gov deposit 1 $(bhcli keys show -a alice)
```

##### 成功返回
```
{
  "proposal_id": "1",
  "depositor": "BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp",
  "amount": [
    {
      "denom": "bht",
      "amount": "10100000000000000000000000"
    }
  ]
}
```

#### 查询某提案的全部抵押信息
```
bhcli query gov deposits [proposal-id][flags] 
```

##### 参数说明

| 名称 | 类型 |参数说明 |
| ------ | ------ | ------ |
| proposal-id | string | proposal id |


##### 示例
```
bhcli query gov deposits 1 
```

##### 成功返回
```
{
  "proposal_id": "1",
  "depositor": "BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp",
  "amount": [
    {
      "denom": "bht",
      "amount": "10100000000000000000000000"
    }
  ]
}
```


#### 查询某voter对某提案的投票信息
```
bhcli query gov vote [proposal-id] [voter-addr] [flags]
```
##### 参数说明

| 名称 | 类型 |参数说明 |
| ------ | ------ | ------ |
| proposal-id | string | proposal id |
| depositer-addr | string | depositer地址 |

##### 示例
```
bhcli query gov vote 1 $(bhcli keys show -a alice)
```
##### 成功返回
```
{
  "proposal_id": "1",
  "voter": "BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp",
  "option": "Yes"
}
```

#### 查询某提案的全部投票信息
```
bhcli query gov votes [proposal-id] [flags]
```
##### 参数说明

| 名称 | 类型 |参数说明 |
| ------ | ------ | ------ |
| proposal-id | string | proposal id |




##### 示例
```
bhcli query gov votes 1 
```
##### 成功返回
```
[
  {
    "proposal_id": "1",
    "voter": "BHZ3uWq8Znb1vLWLtT8EWGrTH424NQkhm7T",
    "option": "No"
  },
  {
    "proposal_id": "1",
    "voter": "BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp",
    "option": "Yes"
  }
]
```



#### 查询某提案的发起者
```
bhcli query gov proposer [proposal-id] [flags] 
```

##### 参数说明

| 名称 | 类型 | 参数说明 |
| ------ | ------ | ------ | 
| proposal-id | string | proposal id |



##### 示例
```
bhcli query gov proposer 1
```

##### 成功返回
```
{
  "proposal_id": "1",
  "proposer": "BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp"
}
```


#### 查询某提案目前投票结果
```
bhcli query gov tally [proposal-id] [flags] 
```

##### 参数说明

| 名称 | 类型 | 参数说明 |
| ------ | ------ | ------ | 
| proposal-id | string | proposal id |

##### 示例
```
bhcli query gov tally 1
```

##### 成功返回
```
{
  "yes": "0",
  "abstain": "0",
  "no": "0",
  "no_with_veto": "0"
}
```

### staking 

#### 查询staking模块的参数
```
bhcli query staking params
```

##### 示例
```
bhcli query staking params
```

##### 成功返回
```
{
  "unbonding_time": "1814400000000000",
  "max_validators": 100,
  "max_entries": 7,
  "bond_denom": "bht",
  "MinSelfDelegation": "5000000000000000000000000"
}
```

#### 查询所有的validators
```
bhcli query staking validators
```
##### 示例
```
bhcli query staking validators
```
##### 成功返回
```
[
  {
    "operator_address": "bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj",
    "consensus_pubkey": "bhvalconspub1zcjduepq9wqxkyh2s6vyna0qncvz5pr7fzj6nqqjs690w23vrvw93cf4dzxsthasln",
    "jailed": false,
    "status": 2,
    "tokens": "100000100000000000000000000",
    "delegator_shares": "100000100000000000000000000.000000000000000000",
    "description": {
      "moniker": "node0",
      "identity": "",
      "website": "",
      "details": ""
    },
    "unbonding_height": "0",
    "unbonding_time": "1970-01-01T00:00:00Z",
    "commission": {
      "commission_rates": {
        "rate": "0.000000000000000000",
        "max_rate": "0.000000000000000000",
        "max_change_rate": "0.000000000000000000"
      },
      "update_time": "2020-03-11T11:00:58.678367Z"
    },
    "min_self_delegation": "5000000000000000000000000"
  }
  ... ...
]
```


#### 查询某一个validator
```
bhcli query staking validator [validator-addr] [flags]
```

##### 参数说明

| 名称 | 类型  | 参数说明 | 
| ------ | ------ | ------ |
| validator-addr | string | 以bhbhvaloper开头的validator地址 |

##### 示例
```
bhcli query staking validator bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj
```

##### 成功返回
```
{
  "operator_address": "bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj",
  "consensus_pubkey": "bhvalconspub1zcjduepq9wqxkyh2s6vyna0qncvz5pr7fzj6nqqjs690w23vrvw93cf4dzxsthasln",
  "jailed": false,
  "status": 2,
  "tokens": "100000100000000000000000000",
  "delegator_shares": "100000100000000000000000000.000000000000000000",
  "description": {
    "moniker": "node0",
    "identity": "",
    "website": "",
    "details": ""
  },
  "unbonding_height": "0",
  "unbonding_time": "1970-01-01T00:00:00Z",
  "commission": {
    "commission_rates": {
      "rate": "0.000000000000000000",
      "max_rate": "0.000000000000000000",
      "max_change_rate": "0.000000000000000000"
    },
    "update_time": "2020-03-11T11:00:58.678367Z"
  },
  "min_self_delegation": "5000000000000000000000000"
}
```

#### 查询某delegtor给某validator的抵押
```
bhcli query staking delegation [delegator-addr] [validator-addr] [flags]
```
##### 参数说明

| 名称 | 类型  | 参数说明 | 
| ------ | ------ | ------ |
| delegator-addr | string | 以BH开头的delegator地址 |
| validator-addr | string | 以bhbhvaloper开头的validator地址 |


##### 示例
```
bhcli query staking delegation BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj
```
##### 成功返回
```
{
  "delegator_address": "BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp",
  "validator_address": "bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj",
  "shares": "120000000000000000000.000000000000000000",
  "balance": "120000000000000000000"
}
```

#### 查询某delegtor所有的抵押
```
bhcli query staking delegations [delegator-addr] [flags]
```

##### 参数说明

| 名称 | 类型  | 参数说明 | 
| ------ | ------ | ------ |
| delegator-addr | string | 以BH开头的delegator地址 |



##### 示例
```
bhcli query staking delegations BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp
```

##### 成功返回
```
[
  {
    "delegator_address": "BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp",
    "validator_address": "bhvaloper136g7jus2k0x7xv7wfusf5npzl5c3uf2cgrwf7z",
    "shares": "50000000000000000000.000000000000000000",
    "balance": "50000000000000000000"
  },
  {
    "delegator_address": "BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp",
    "validator_address": "bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj",
    "shares": "120000000000000000000.000000000000000000",
    "balance": "120000000000000000000"
  }
]
```

#### 查询某delegtor给某validator的正在解冻的抵押
```
bhcli query staking unbonding-delegation [delegator-addr] [validator-addr] [flags]
```

##### 参数说明

| 名称 | 类型  | 参数说明 | 
| ------ | ------ | ------ |
| delegator-addr | string | 以BH开头的delegator地址 |
| validator-addr | string | 以bhbhvaloper开头的validator地址 |

##### 示例
```
bhcli query staking unbonding-delegation BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj
```

##### 成功返回
```
{
  "delegator_address": "BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp",
  "validator_address": "bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj",
  "entries": [
    {
      "creation_height": "5931",
      "completion_time": "2020-04-03T08:23:33.8255297Z",
      "initial_balance": "30000000000000000000",
      "balance": "30000000000000000000"
    }
  ]
}
```


#### 查询某delegtor所有的正在解冻的抵押
```
bhcli query staking unbonding-delegations [delegator-addr] [flags]
```
##### 参数说明

| 名称 | 类型 | 参数说明 |
| ------ | ------ | ------ |
| delegator-addr | string | 以BH开头的delegator地址 |



##### 示例
```
bhcli query staking unbonding-delegations BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp
```
##### 成功返回
```
[
  {
    "delegator_address": "BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp",
    "validator_address": "bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj",
    "entries": [
      {
        "creation_height": "5931",
        "completion_time": "2020-04-03T08:23:33.8255297Z",
        "initial_balance": "30000000000000000000",
        "balance": "30000000000000000000"
      }
    ]
  }
]
```

#### 查询某delegtor redeleagte的抵押
```
bhcli query staking redelegation [delegator-addr] [src-validator-addr] [dst-validator-addr] [flags]
```
##### 参数说明

| 名称 | 类型  | 参数说明 | 
| ------ | ------ | ------ |
| delegator-addr | string | 以BH开头的delegator地址 |
| src-validator-add | string | 以bhbhvaloper开头的源validator地址 |
| dst-validator-addr | string | 以bhbhvaloper开头的目的validator地址 |

##### 示例
```
query staking redelegation BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj bhvaloper1ksn6eszxp4v2sfrf96s5ded4zz9cr9u46uy0hz
```

##### 成功返回
```
[
  {
    "delegator_address": "BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp",
    "validator_src_address": "bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj",
    "validator_dst_address": "bhvaloper136g7jus2k0x7xv7wfusf5npzl5c3uf2cgrwf7z",
    "entries": [
      {
        "creation_height": 5891,
        "completion_time": "2020-04-03T08:19:58.6984724Z",
        "initial_balance": "50000000000000000000",
        "shares_dst": "50000000000000000000.000000000000000000",
        "balance": "50000000000000000000"
      }
    ]
  }
]
```

#### 查询某delegtor所有redelegate抵押
```
bhcli query staking redelegations 
```

##### 示例
```
bhcli query staking redelegations BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp
```

##### 成功返回
```
[
  {
    "delegator_address": "BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp",
    "validator_src_address": "bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj",
    "validator_dst_address": "bhvaloper136g7jus2k0x7xv7wfusf5npzl5c3uf2cgrwf7z",
    "entries": [
      {
        "creation_height": 5891,
        "completion_time": "2020-04-03T08:19:58.6984724Z",
        "initial_balance": "50000000000000000000",
        "shares_dst": "50000000000000000000.000000000000000000",
        "balance": "50000000000000000000"
      }
    ]
  }
]
```

#### 查询validator收到的所有抵押
```
  bhcli query staking delegations-to [validator-addr] [flags]
```

##### 参数说明

| 名称 | 类型  | 参数说明 | 
| ------ | ------ | ------ |
| validator-addr | string | 以bhbhvaloper开头的validator地址 |


##### 示例
```
 bhcli query staking delegations-to bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj
```

##### 成功返回
```
[
  {
    "delegator_address": "BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp",
    "validator_address": "bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj",
    "shares": "120000000000000000000.000000000000000000",
    "balance": "120000000000000000000"
  },
  {
    "delegator_address": "BHj2wujKtAxw9XZMA7zDDvjGqKjoYUdw1FZ",
    "validator_address": "bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj",
    "shares": "100000000000000000000000000.000000000000000000",
    "balance": "100000000000000000000000000"
  }
]
```

#### 查询所有从某validator redelegate给其他validator 的抵押
```
bhcli query staking redelegations-from [validator-addr] [flags]
```
##### 参数说明

| 名称 | 类型 |参数说明 |
| ------ | ------ | ------ |
| validator-addr | string | 以bhbhvaloper开头的validator地址 |

##### 示例
```
bhcli query staking redelegations-from bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj
```

##### 成功返回
```
[
  {
    "delegator_address": "BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp",
    "validator_src_address": "bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj",
    "validator_dst_address": "bhvaloper136g7jus2k0x7xv7wfusf5npzl5c3uf2cgrwf7z",
    "entries": [
      {
        "creation_height": 5891,
        "completion_time": "2020-04-03T08:19:58.6984724Z",
        "initial_balance": "50000000000000000000",
        "shares_dst": "50000000000000000000.000000000000000000",
        "balance": "50000000000000000000"
      }
    ]
  }
]
```


#### 查询validator正在解冻的抵押
```
bhcli query staking unbonding-delegations-from [validator-addr] [flags]
```
##### 参数说明

| 名称 | 类型 |参数说明 |
| ------ | ------ | ------ |
| validator-addr | string | 以bhbhvaloper开头的validator地址 |

##### 示例
```
bhcli query staking unbonding-delegations-from bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj
```

##### 成功返回
```
[
  {
    "delegator_address": "BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp",
    "validator_address": "bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj",
    "entries": [
      {
        "creation_height": "5931",
        "completion_time": "2020-04-03T08:23:33.8255297Z",
        "initial_balance": "30000000000000000000",
        "balance": "30000000000000000000"
      }
    ]
  }
]
```


#### 查询staking pool中的金额
```
$bhcli query staking pool
```
##### 示例
```
$bhcli query staking pool
```

##### 成功返回
```
{
  "not_bonded_tokens": "30000000000000000000",
  "bonded_tokens": "400000170000000000000000000"
}
```


### distribution 

#### 查询distribution的参数
```
bhcli query distribution params
```
##### 示例
```
bhcli query distribution params
```
##### 成功返回
```
{
  "community_tax": "0.020000000000000000",
  "base_proposer_reward": "0.010000000000000000",
  "bonus_proposer_reward": "0.040000000000000000",
  "withdraw_addr_enabled": true
}
```

#### 查询validator-outstanding-rewards
```
bhcli query distribution validator-outstanding-rewards [validator] [flags]
```
##### 参数说明

| 名称 | 类型 | 参数说明 |
| ------ | ------ | ------ |
| validator | string | 以bhbhvaloper开头的validator地址 |



##### 示例
```
bhcli query distribution validator-outstanding-rewards bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj
```
##### 成功返回
```
[
  {
    "denom": "bht",
    "amount": "2660287954396406984212.455000000000000000"
  }
]
```

#### 查询validator的commisssion
```
 bhcli query distribution commission [validator] [flags]
```
##### 参数说明

| 名称 | 类型 | 参数说明 |
| ------ | ------ | ------ |
| validator | string | 以bhbhvaloper开头的validator地址 |

##### 示例
```
bhcli query distribution commission bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj
```
##### 成功返回
```
null
```
注：因为目前几个validator 的commission都设置为0

#### 查询validator的slashes
```
bhcli query distribution slashes [validator] [start-height] [end-height] [flags]
```
##### 参数说明

| 名称 | 类型 | 参数说明 |
| ------ | ------ | ------ |
| validator | string | 以bhbhvaloper开头的validator地址 |
| start-height | string | start hegiht |
| end-height | string | end hegiht |

##### 示例
```
bhcli query distribution slashes bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj 0 100
```

##### 成功返回
```
null
```


#### 查询validator的rewards
```
bhcli query distribution rewards [delegator-addr] [<validator-addr>] [flags]
```
##### 参数说明

| 名称 | 类型 | 参数说明 |
| ------ | ------ | ------ |
| delegator-addr | string | 以BH开头的delegator地址 |
| validator-addr | string | 以bhbhvaloper开头的validator地址,可选 |


##### 示例
```
bhcli query distribution rewards BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj
```
##### 成功返回
```
[
  {
    "denom": "bht",
    "amount": "962401463225280.000000000000000000"
  }
]
```

#### 查询community-pool
```
bhcli query distribution community-pool
```
##### 示例
```
bhcli query distribution community-pool
```
##### 成功返回
```
[
  {
    "denom": "bht",
    "amount": "219939930488250056843.400000000000000000"
  }
]
```


### slashing 

#### 查询slashing的参数
```
bhcli query slashing params
```
##### 示例
```
bhcli query slashing params
```
##### 成功返回

```
{
  "max_evidence_age": "120000000000",
  "signed_blocks_window": "100",
  "min_signed_per_window": "0.500000000000000000",
  "downtime_jail_duration": "600000000000",
  "slash_fraction_double_sign": "0.050000000000000000",
  "slash_fraction_downtime": "0.010000000000000000"
}
```

#### 查询一个validator 的签名信息

```
bhcli query slashing signing-info [validator-conspub] [flags]
```

##### 参数说明

| 名称 | 类型 | 参数说明 |
| ------ | ------ | ------ |
| validator-conspub | string | 以bhvalconspub开头的validator 公钥 |

##### 示例

```
bhcli query slashing signing-info bhvalconspub1zcjduepq69plcv4nzg27qashf328q0p6uc8cdpl4u3fz5sd2ugz34nk0u4ws2zrp0f
```
##### 成功返回

```
{
  "address": "bhvalcons1h0muy2683gyp6ra2qph9hxwdfmxzw6x4xtkm8m",
  "start_height": "0",
  "index_offset": "8606",
  "jailed_until": "1970-01-01T00:00:00Z",
  "tombstoned": false,
  "missed_blocks_counter": "0"
}
```



### cu
#### 查询某个cu的信息
```
bhcli query cu cuinfo [cu_addr][flags] 
```
##### 参数说明

| 名称 | 类型  | 参数说明 | 
| ------ | ------ | ------ |
| cu-addr | string | 以BH开头的托管托单元地址 |

##### 示例
```
bhcli query cu cuinfo $(bhcli keys show -a alice)
```
##### 成功返回
```

{
  "type": "bhchain/CustodianUnit",
  "value": {
    "cu_type": "1",
    "address": "BHhhzxqNNjw3qx4ZjaR9mnJeLRC1FxPWEyp",
    "public_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "AwvzJMjkXTRO9jmkEHiLi/2BHpwLuAR+SohLW2t3vwe/"
    },
    "sequence": "8",
    "coins": [
      {
        "denom": "bht",
        "amount": "299999974110000000000000000"
      },
      {
        "denom": "eth",
        "amount": "17800000000000000"
      }
    ],
    "coins_hold": [
      {
        "denom": "eth",
        "amount": "2200000000000000"
      }
    ],
    "assets": [
      {
        "denom": "eth",
        "address": "0x0B2dE9E53f794A51D133afae5cF6142DA4130Fb3",
        "enbale_sendtx": false
      }
    ],
    "asset_coins": [
      {
        "denom": "eth",
        "amount": "20000000000000000"
      }
    ],
    "asset_coins_hold": [],
    "cu_number": "0",
    "asset_pubkey": "Ats0/JuoM9z3VhMGRoUGoxXiZ+Uc9NUooVg+FtJL+Hrf",
    "gas_used": [],
    "gas_received": []
  }
}
```



## tx
### keygen
#### 创建运营托管单元（OPCU）
```bash
bhcli tx keygen newopcu [from_key_or_address] [symbol] [Op_CU_address]
```
##### 参数说明

| 名称 | 类型  | 参数说明 | 
| ------ | ------ | ------ |
| --from_key_or_address | string | newopcu交易发起者地址 |
| --symbol | string | 币种 |
| --to | string | OPCU地址 |

##### 示例
创建一个eth运营托管单元，地址为BHiLmdKcdt7k98BizNi4mhRgrkrtZYmXWj9, 该地址必须是未被使用的地址
```
bhcli tx keygen newopcu BHj2wujKtAxw9XZMA7zDDvjGqKjoYUdw1FZ eth BHiLmdKcdt7k98BizNi4mhRgrkrtZYmXWj9 --chain-id bhchain-testnet --gas-prices 1000000000000.0bht --home ../testnetdocker/node0/bhcli
```
##### 成功返回
```
{
  "chain_id": "bhchain-testnet",
  "cu_number": "0",
  "sequence": "664",
  "fee": {
    "amount": [
      {
        "denom": "bht",
        "amount": "200000000000000000"
      }
    ],
    "gas": "200000"
  },
  "msgs": [
    {
      "type": "bhchain/keygen/MsgNewOpCU",
      "value": {
        "Symbol": "eth",
        "From": "BHj2wujKtAxw9XZMA7zDDvjGqKjoYUdw1FZ",
        "OpCUAddress": "BHiLmdKcdt7k98BizNi4mhRgrkrtZYmXWj9"
      }
    }
  ],
  "memo": ""
}

confirm transaction before signing and broadcasting [y/N]: y
Password to sign with 'node0':<输入密码>
height: 0
txhash: B8FEF2E621686136882ADA19C939D959982D979C13BB51D3ACA29C4C964AC777
code: 0
data: ""
rawlog: '[{"msg_index":0,"success":true,"log":"","events":[{"type":"message","attributes":[{"key":"action","value":"new_op_cu"}]}]}]'
logs:
- msgindex: 0
  success: true
  log: ""
  events:
  - type: message
    attributes:
    - key: action
      value: new_op_cu
info: ""
gaswanted: 0
gasused: 0
codespace: ""
tx: null
timestamp: ""
events: []
```

#### 为托管单元（CU）生成币种地址
```bash
keygen [from_key_or_address] [symbol] [to]
```
##### 参数说明

| 名称 | 类型  | 参数说明 | 
| ------ | ------ | ------ |
| --from_key_or_address | string | keygen交易发起者地址 |
| --symbol | string | 币种 |
| --to | string | 创建币种地址的所有者 |

##### 示例
为BHiLmdKcdt7k98BizNi4mhRgrkrtZYmXWj9 生成eth地址 
```
bhcli tx keygen keygen BHj2wujKtAxw9XZMA7zDDvjGqKjoYUdw1FZ eth BHiLmdKcdt7k98BizNi4mhRgrkrtZYmXWj9 --chain-id bhchain-testnet --gas-prices 1000000000000.0bht --home ../testnetdocker/node0/bhcli
```
##### 成功返回
```
{
  "chain_id": "bhchain-testnet",
  "cu_number": "0",
  "sequence": "603",
  "fee": {
    "amount": [
      {
        "denom": "bht",
        "amount": "200000000000000000"
      }
    ],
    "gas": "200000"
  },
  "msgs": [
    {
      "type": "bhchain/keygen/MsgKeyGen",
      "value": {
        "OrderId": "8aa29c69-2cd4-4dde-bb5c-273757bfdd6e",
        "Symbol": "eth",
        "From": "BHj2wujKtAxw9XZMA7zDDvjGqKjoYUdw1FZ",
        "To": "BHiLmdKcdt7k98BizNi4mhRgrkrtZYmXWj9"
      }
    }
  ],
  "memo": ""
}

confirm transaction before signing and broadcasting [y/N]: y
Password to sign with 'node0':<输入密码>
height: 0
txhash: 4ABC263EFFAC364ED966EE4654ADEC050D6A1C2886B229CE13556010111531E9
code: 4
data: ""
rawlog: '{"codespace":"bhchain_base","code":4,"message":"signature verification failed;
  verify correct CU sequence and chain-id"}'
logs: []
info: ""
gaswanted: 0
gasused: 0
codespace: ""
tx: null
timestamp: ""
events: []
```

### gov
#### 发起一个提案
```
bhcli tx gov submit-proposal --title="Test Proposal Title" --description="Test Proposal Contents" --type="Text" --deposit="10bht" --from mykey --gas-prices 1000000000000.0bht
```
或者
```
bhcli tx gov submit-proposal --proposal="path/to/proposal.json" --from mykey --gas-prices 1000000000000.0bht
```

##### 参数说明

| 名称 | 类型  | 参数说明 | 
| ------ | ------ | ------ |
| --title | string | 提案的标题 |
| --description | string | 提案的内容 |
| --type | string | 发起提案的类型（这里指定为Text |
| --from | string | 提案发起者 |

##### 示例
```
bhcli tx gov submit-proposal --title="Test Proposal Title" --description="Test Proposal Contents" --type="Text" --deposit="100000000000000000000000bht" --from alice --gas-prices 1000000000000.0bht
```

##### 成功返回
```
{
  "height": "0",
  "txhash": "0CC5E052CBCEDE6167BEF4B818C2D728D52857C0C9514211BD389FCAD1723F03",
  "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"submit_proposal\"}]}]}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
      "log": "",
      "events": [
        {
          "type": "message",
          "attributes": [
            {
              "key": "action",
              "value": "submit_proposal"
            }
          ]
        }
      ]
    }
  ]
}
```
#### 为某个提案抵押资金
```
bhcli tx gov deposit [proposal-id] [amount]
```

##### 参数说明

| 名称 | 类型 |参数说明 |
| ------ | ------ | ------ |
| proposal-id | string | proposal id |
| amount | string | 抵押的资金 |


##### 示例
```
bhcli tx gov deposit 1 10000000000000000000000000bht --gas-prices 1000000000000.0bht --from alice
```
##### 成功返回
```
{
  "height": "0",
  "txhash": "83729758C6E2986772AED8CFB244B7954CF1EA5C044577101226A0EBFDCC4E68",
  "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"deposit\"}]}]}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
      "log": "",
      "events": [
        {
          "type": "message",
          "attributes": [
            {
              "key": "action",
              "value": "deposit"
            }
          ]
        }
      ]
    }
  ]
}
```

#### 为某个提案投票
```
bhcli tx gov vote [proposal-id] [option] [flags]
```
##### 参数说明

| 名称 | 类型  | 参数说明 | 
| ------ | ------ | ------ |
| proposal-id | string | proposal id |
| options | string | 投票选项yes/no/abstain/nowithveto |



##### 示例
```
bhcli tx gov vote 1 yes --from alice --gas-prices 1000000000000.0bht
```
##### 成功返回
```
{
  "height": "0",
  "txhash": "479517D2CDC084C0393DD4E9DB2B7FDDD6A1E9C166EAF893ABAB089B27A8F667",
  "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"vote\"}]}]}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
      "log": "",
      "events": [
        {
          "type": "message",
          "attributes": [
            {
              "key": "action",
              "value": "vote"
            }
          ]
        }
      ]
    }
  ]
}
```

### staking
#### 将资产抵押给validator
 ```
 bhcli tx staking delegate [validator-addr] [amount] [flags]
 ```
##### 参数说明

| 名称 | 类型  | 参数说明 | 
| ------ | ------ | ------ |
| validator-addr | string | 以bhvaloper开头的validator地址 |
| amount | string | 币种以及金额 |

##### 示例

```
bhcli tx staking delegate bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj  100000000000000000000bht --from alice --gas-prices 1000000000000.0bht
```
##### 成功返回
```
{
  "height": "0",
  "txhash": "127DE69768E413CDBADB15F3A220DD22FE5D1984F1143D525EBE934A6D4DD171",
  "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"delegate\"}]}]}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
      "log": "",
      "events": [
        {
          "type": "message",
          "attributes": [
            {
              "key": "action",
              "value": "delegate"
            }
          ]
        }
      ]
    }
  ]
}
```

#### 将资产从一个validator 抵押给另外一个validator
 ```
bhcli tx staking redelegate [src-validator-addr] [dst-validator-addr] [amount] [flag]
 ```
##### 参数说明


| 名称 | 类型  | 参数说明 | 
| ------ | ------ | ------ |
| src-validator-addr | string | 以bhvaloper开头的源validator地址 |
| dst-validator-addr | string | 以bhvaloper开头的目的validator地址 |
| amount | string | 币种以及金额 |


##### 示例

```
bhcli tx staking redelegate bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj bhvaloper136g7jus2k0x7xv7wfusf5npzl5c3uf2cgrwf7z 50000000000000000000bht --from alice --gas-prices 1000000000000.0bht
```
##### 成功返回
```
{
  "height": "0",
  "txhash": "1B72BF06683454C90E4C956B5AE865F782CF9777B71481CA9211CB92236AA7A1",
  "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"begin_redelegate\"}]}]}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
      "log": "",
      "events": [
        {
          "type": "message",
          "attributes": [
            {
              "key": "action",
              "value": "begin_redelegate"
            }
          ]
        }
      ]
    }
  ]
}
```


### distribution

#### 设置delegator rewards 的受益地址
```
 bhcli tx distribution set-withdraw-addr [withdraw-addr] [flags]
```
##### 参数说明

| 名称 | 类型 | 参数说明 |
| ------ | ------ | ------ |
| withdraw-addr | string | 以BH开头受益托管单元地址 |

##### 示例
```
 bhcli tx distribution set-withdraw-addr BHZQPXRfihTbCpAmkP3EeiDAV5TU31ZiQ5P --from mykey --gas-prices 1000000000000.0bht

```

##### 成功返回
```
{
  "height": "0",
  "txhash": "24476645A437C61A6560E1B3C12A94A21265223AE20649148EA238BD323C84C8",
  "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"set_withdraw_address\"}]}]}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
      "log": "",
      "events": [
        {
          "type": "message",
          "attributes": [
            {
              "key": "action",
              "value": "set_withdraw_address"
            }
          ]
        }
      ]
    }
  ]
}
```

#### 从某个validator提取抵押收益
```
bhcli tx distribution withdraw-rewards [validator-addr] [flags]
```

##### 参数说明

| 名称 | 类型 | 参数说明 |
| ------ | ------ | ------ |
| validator-addr | string | 以bhbhvaloper开头的validator地址 |

##### 示例
```
bhcli tx distribution withdraw-rewards bhvaloper1lh86pkhl6nrvmyezmncwdvhmnr0hj6nlk0caaj --from alice --gas-prices 1000000000000.0bht
```

##### 成功返回
```
{
  "height": "0",
  "txhash": "FE63EC4BE20EF947F58C847DF935F6951155F4F9DD1AE519A7F9FBAF6925B7F5",
  "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"withdraw_delegator_reward\"}]}]}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
      "log": "",
      "events": [
        {
          "type": "message",
          "attributes": [
            {
              "key": "action",
              "value": "withdraw_delegator_reward"
            }
          ]
        }
      ]
    }
  ]
}
```
#### 从所有validator提取抵押收益
```
bhcli tx distribution withdraw-all-rewards [flags]
```

##### 示例
```
bhcli tx distribution withdraw-all-rewards --from alice --gas-prices 1000000000000.0bht
```
##### 成功返回
```
{
  "height": "0",
  "txhash": "E8602B91CC973EBB4369277C18364CFB1663BED3F1E565FFBE19C0D2AE47F7BE",
  "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"withdraw_delegator_reward\"}]}]},{\"msg_index\":1,\"success\":true,\"log\":\"\",\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"withdraw_delegator_reward\"},{\"key\":\"action\",\"value\":\"withdraw_delegator_reward\"}]}]}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
      "log": "",
      "events": [
        {
          "type": "message",
          "attributes": [
            {
              "key": "action",
              "value": "withdraw_delegator_reward"
            }
          ]
        }
      ]
    },
    {
      "msg_index": 1,
      "success": true,
      "log": "",
      "events": [
        {
          "type": "message",
          "attributes": [
            {
              "key": "action",
              "value": "withdraw_delegator_reward"
            },
            {
              "key": "action",
              "value": "withdraw_delegator_reward"
            }
          ]
        }
      ]
    }
  ]
}
```



### transfer 
#### bhex系统内部转账 

```
bhcli tx transfer send [from] [to][amount][flags] 
```
##### 参数说明

| 名称 | 类型  | 参数说明 | 
| ------ | ------ | ------ |
| from | string | 资产的所有者 |
| to | string | 转入的托管单元地址 |
| amount | string | 币种以及金额，多个资产是以逗号分隔。例如100bht，2btc |



##### 示例
```
bhcli tx transfer send alice  BHZ3uWq8Znb1vLWLtT8EWGrTH424NQkhm7T  1000000000000000bht  --chain-id bhchain-testnet  --gas-prices 1000000000000.0bht
```

#### 成功返回
```
{
  "height": "0",
  "txhash": "D6E4AD62656EAF9FE65C651CEFACF2C974D19B9E5C3348A00A9E3CD1A1BF2F91",
  "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"send\"}]}]}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
      "log": "",
      "events": [
        {
          "type": "message",
          "attributes": [
            {
              "key": "action",
              "value": "send"
            }
          ]
        }
      ]
    }
  ]
}

```

#### 将外链资产充值到bhex

```
bhcli tx transfer deposit [from_key_or_address] [toCU_address] [to_address] [coin] [txhash] [index] [memo] [height] [flags]
```
##### 参数说明

| 名称 | 类型  | 参数说明 | 
| ------ | ------ | ------ |
| from_key_or_address | string | 充值的发起人，可以是toCU的所有者也可以是其他人 |
| to_cu | string | 被充值的托管单元地址 |
| to_address | string | 被充值的托管单元地址对应币种的外链(例如:btc eth)地址 |
| amount | string | 币种以及金额 |
| hash | string | 外链交易hash |
| index | string | 外链交易索引，对于utxo类型资产, index 等于Vout中的index值;对于账户类型资产，index = 0 |
| memo | string | 外链交易中附带的memo |
| height | string | 外链交易发生的区块高度 |




##### 示例
```
bhcli tx transfer deposit alice $(bhcli keys show -a bob) 0x6537f7fb0064aaa4b5b9f379d24133027155b727 10000000000000000eth 0x228409bb2999911b94f0513f101f3fcf212058b7af18c88c625b41ddf20a0c6b 0 memo 7505327 --chain-id bhchain-testnet --gas-prices 1000000000000.0bht
```

##### 成功返回
```
{ 
height: 0
txhash: E81EC801B96C99E99BA2EAA73624AF5FAA7A0356894846BB11C70D57B62937AD
code: 0
data: ""
rawlog: '[{"msg_index":0,"success":true,"log":"","events":[{"type":"message","attributes":[{"key":"action","value":"deposit"}]}]}]'
logs:
- msgindex: 0
  success: true
  log: ""
  events:
  - type: message
    attributes:
    - key: action
      value: deposit
info: ""
gaswanted: 0
gasused: 0
codespace: ""
tx: null
timestamp: ""
events: []
}
```




#### 将资产提现到外链地址
```
bhcli tx transfer withdrawal [from_key_or_address] [to_address] [amount] [gas] [flags]
```
##### 参数说明

| 名称 | 类型  | 参数说明 | 
| ------ | ------ | ------ |
| from_key_or_address | string | 充值的发起人，可以是toCU的所有者也可以是其他人 |
| to_address | string | 被充值的托管单元地址对应币种的外链(例如:btc eth)地址 |
| amount | string | 币种以及金额 |
| gas | string | 以外链币计价的手续费 |


##### 示例
```
bhcli tx transfer withdrawal --chain-id bhchain-testnet alice  0xc96d141c9110a8E61eD62caaD8A7c858dB15B82c  1200000000000000eth  1000000000000000 --gas-prices 1000000000000.0bht
```
##### 成功返回
```
{
  "height": "0",
  "txhash": "F240EB278D946EA9C1DD999A56E54D8ADD3BE16FA9A93F5CF9BD8DE4DAD179DA",
  "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"withdrawal\"}]}]}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
      "log": "",
      "events": [
        {
          "type": "message",
          "attributes": [
            {
              "key": "action",
              "value": "withdrawal"
            }
          ]
        }
      ]
    }
  ]
}

```

## rest-server
从本地启动一个rest server
```
bhcli rest-server [flags] 
```
| 名称 | 类型  | flag说明 | 
| ------ | ------ | ------ |
| laddr string | string | rest server监听地址，(default "tcp://localhost:1317") |
| max-open | uint | 最大连接数 |
| node | string | 链节点地址<host>:<port>，(default "tcp://localhost:26657") |
| trust-node | string | 信任连接的节点 |


### 示例
```shell
bhcli rest-server --home node0/bhcli --chain-id bhchain-testnet --node tcp://127.0.0.1:26657 --trust-node true 
```
### 正常返回
```
I[2020-03-14|09:18:04.726] Starting application REST service (chain-id: "bhchain-testnet")... module=rest-server
I[2020-03-14|09:18:04.727] Starting RPC HTTP server on 127.0.0.1:1317   module=rest-server
```

## keys

本地密钥库主要包含以下指令：
* `bhcli keys add`     [新增密钥](#新增) (#列表)
* `bhcli keys list`    [显示密钥列表](#列表)
* `bhcli keys update`  [更新密钥保存密码](#更新)
* `bhcli keys delete`  [从密钥库删除密钥](#删除)
* `bhcli keys import`  [导入密钥](#导入)
* `bhcli keys export`  [导出密钥](#导出)

> 密钥库为本地存储，默认存储位置为：$HOME/.bhcli/keys/，删除存储文件会清空本地存储所有私钥。通过`keys`相关指令操作密钥不影响QOS网络中账户状态，请妥善保管账户私钥信息。

#### 新增

`bhcli keys add <key_name>`

<key_name>可随意填写，仅作为本地密钥库密钥区分。

如下指令将生成一个名字为`Alice`的密钥到本地密钥库：
```bash
$ bhcli keys add Alice
Enter a passphrase to encrypt your key to disk:<输入密码>
Repeat the passphrase:<重复上面输入的密码>
NAME:	TYPE:	ADDRESS:						PUBKEY:
- name: alice
  type: local
  address: BHbKoCY3f5q22sCkHTFk22w3yfQJZEjVwNJ
  pubkey: bhpub1addwnpepq2ngc3wxzlrfhfp2h49c0l60zlnl8qqlweuy6nl6fwxh3vzf8nvz6hsygrc
  mnemonic: ""
  threshold: 0
  pubkeys: []


**Important** write this mnemonic phrase in a safe place.
It is the only way to recover your CU if you ever forget your password.

rare nuclear foster thunder wonder core section file utility service quiz correct lion frost piano split aisle weather depth main trumpet lobster fire connect
```
其中`BHbKoCY3f5q22sCkHTFk22w3yfQJZEjVwNJ`为适用于QOS网络的账户地址，`bhpub1addwnpepq2ngc3wxzlrfhfp2h49c0l60zlnl8qqlweuy6nl6fwxh3vzf8nvz6hsygrc`为账户公钥信息，`rare nuclear foster thunder wonder core section file utility service quiz correct lion frost piano split aisle weather depth main trumpet lobster fire connect`为助记词，可用于账户私钥找回，请妥善保管助记词。

#### 列表

`bhcli keys list`
```bash
$ bhcli keys list
N- name: alice
  type: local
  address: BHbKoCY3f5q22sCkHTFk22w3yfQJZEjVwNJ
  pubkey: bhpub1addwnpepq2ngc3wxzlrfhfp2h49c0l60zlnl8qqlweuy6nl6fwxh3vzf8nvz6hsygrc
  mnemonic: ""
  threshold: 0
  pubkeys: []
- name: nouse
  type: local
  address: BHa9VmabsbrQmRErscAbUv9DEWykF3fYToF
  pubkey: bhpub1addwnpepq2e7rss6z90sc0l8cgmees640sgkg65fa08jer3qaf390m0kt2fugn9ka9n
  mnemonic: ""
  threshold: 0
  pubkeys: []
```

#### 更新

`bhcli keys update <key_name>`

更新`Alice`存储密码：
```bash
$ bhcli keys update Alice
Enter the current passphrase:<输入当前密码>
Enter the new passphrase:<输入新密码>
Repeat the new passphrase:<重复新密码>
Password successfully updated!
```

#### 导出

`bhcli keys export <key_name>`

导出`Alice`密钥信息：
```bash
bhcli keys export Alice
Enter passphrase to decrypt your key:<输入当前密码>
Enter passphrase to encrypt the exported key:<输入密码>
-----BEGIN TENDERMINT PRIVATE KEY-----
salt: A6528A0F9D47D2A8E949037D27A4BDD8
kdf: bcrypt

3DgFM6oCq7DWwxxjkzEvk3M53y3UnP5g3cAEFR7oYwvibG6+XBbdhncX1vKFeK/m
79ofswcWI/VRuzxg9s+NXwnRYUFU4tLYPYI58FA=
=JCP8
-----END TENDERMINT PRIVATE KEY-----
```

#### 删除

`bhcli keys delete <key_name>`

删除`Alice`密钥信息：
```bash
$ bhcli keys delete alice
DANGER - enter password to permanently delete key:<输入密码>
Key deleted forever (uh oh!)
```

#### 导入

`bhcli keys import Alice --file <私钥文件路径>`

把上面通过`export`导出的私钥存为alice.pri文件：
```bash
bhcli keys import alice ./alice.pri 
Enter passphrase to decrypt your key:<输入密码>
```
## version
显示version信息

##### 示例

##### 成功返回

## help
显示help信息

##### 示例
```
bhcli help
```
##### 成功返回
```
Command line interface for interacting with bhchain

Usage:
  bhcli [command]

Available Commands:
  status      Query remote node for status
  config      Create or query an application CLI configuration file
  query       Querying subcommands
  tx          Transactions subcommands

  rest-server Start LCD (light-client daemon), a local REST server

  keys        Add or view local private keys

  version     Print the app version
  help        Help about any command
```