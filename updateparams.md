## Motivation

Since the mainnet launch the global blockchain parameters were left as default, and now with a recent increase of the usage, the users noticed that the system contract is triggering the CPU congestion mode too early. As soon as a block hits 10% of the total 200ms of CPU time allowed per block, the CPU allocation algorithm switches to the congestion mode and every user if left with his share of the remaining allocation based on their stake in proportion to the whole network stake. What ended up happening is that while the actual CPU usage of the validators is very low, the CPU price became higher.

This proposal aims to change the current value for `target_block_cpu_usage_pct` from `1000` (10%) to `2000` (20%), tests were performed on the CryptoKylin testnet showing that the algorithm transition happens in a much smoother way and also allowed more resources from the nodes to be used. Test reports are available here: 

Ideally, this value should be updated considering the growth of usage on the mainnet, and it is a safe parameter to revert at any time. 

## Proposal Review

The only action is eosio::setparams, so it can be easily reviewed with `cleos multisig review eosriobrazil updateparams`, which should return:

```
{
  "proposal_name": "updateparams",
  "packed_transaction": "3abdca5b00000000000000000000010000000000ea30550000c0d25c53b3c2010000000000ea305500000000a8ed3232440000100000000000e8030000000008000c000000f40100001400000064000000400d0300d0070000f049020064000000100e00005802000080533b00001000000400060000",
  "transaction": {
    "expiration": "2018-10-20T05:29:30",
    "ref_block_num": 0,
    "ref_block_prefix": 0,
    "max_net_usage_words": 0,
    "max_cpu_usage_ms": 0,
    "delay_sec": 0,
    "context_free_actions": [],
    "actions": [{
        "account": "eosio",
        "name": "setparams",
        "authorization": [{
            "actor": "eosio",
            "permission": "active"
          }
        ],
        "data": {
          "params": {
            "max_block_net_usage": 1048576,
            "target_block_net_usage_pct": 1000,
            "max_transaction_net_usage": 524288,
            "base_per_transaction_net_usage": 12,
            "net_usage_leeway": 500,
            "context_free_discount_net_usage_num": 20,
            "context_free_discount_net_usage_den": 100,
            "max_block_cpu_usage": 200000,
            "target_block_cpu_usage_pct": 2000,
            "max_transaction_cpu_usage": 150000,
            "min_transaction_cpu_usage": 100,
            "max_transaction_lifetime": 3600,
            "deferred_trx_expiration_window": 600,
            "max_transaction_delay": 3888000,
            "max_inline_action_size": 4096,
            "max_inline_action_depth": 4,
            "max_authority_depth": 6
          }
        },
        "hex_data": "0000100000000000e8030000000008000c000000f40100001400000064000000400d0300d0070000f049020064000000100e00005802000080533b000010000004000600"
      }
    ],
    "transaction_extensions": []
  }
}
```
On-chain values can be retrived usign `cleos get table eosio eosio global`, there are more parameters that are extended by the system contract, so they don't need to be passed on the setparams action.

# 中文版 (EOS Asia 翻译)

## 提案动机

自从主网启动以来，多数链上全局配置参数均被保留为默认值。随着用户的增长和最近的使用量的增加，我们开始注意到系统合同过早地触发了CPU拥塞模式。 一旦块达到每块允许的总200ms CPU时间的10％，CPU分配算法就会切换到拥塞模式，每个用户能使用的资源会根据他们与整个网络抵押的比例的份额。实际上，当链上CPU使用10%时，节点的实际CPU使用率是非常低的，过早的触发拥塞模式导致发起链上任何请求需要的CPU价格变得更高。

该提案旨在将`target_block_cpu_usage_pct`的当前值从`1000`（10％）更改为`2000`（20％），该提案已经在CryptoKylin Testnet上测试过，也成功让分配算法利用更多的节点实际资源。 测试报告可在此处获得：

[insert report link here]

该配置也需要随着主网使用量的变化做更改，此改变也可以随时安全撤回。

## 审核提案

提案唯一发起的 action 是 eosio::setparams，你可以通过调用 `cleos multisig review eosriobrazil updateparams` 进行审核：

```
{
  "proposal_name": "updateparams",
  "packed_transaction": "3abdca5b00000000000000000000010000000000ea30550000c0d25c53b3c2010000000000ea305500000000a8ed3232440000100000000000e8030000000008000c000000f40100001400000064000000400d0300d0070000f049020064000000100e00005802000080533b00001000000400060000",
  "transaction": {
    "expiration": "2018-10-20T05:29:30",
    "ref_block_num": 0,
    "ref_block_prefix": 0,
    "max_net_usage_words": 0,
    "max_cpu_usage_ms": 0,
    "delay_sec": 0,
    "context_free_actions": [],
    "actions": [{
        "account": "eosio",
        "name": "setparams",
        "authorization": [{
            "actor": "eosio",
            "permission": "active"
          }
        ],
        "data": {
          "params": {
            "max_block_net_usage": 1048576,
            "target_block_net_usage_pct": 1000,
            "max_transaction_net_usage": 524288,
            "base_per_transaction_net_usage": 12,
            "net_usage_leeway": 500,
            "context_free_discount_net_usage_num": 20,
            "context_free_discount_net_usage_den": 100,
            "max_block_cpu_usage": 200000,
            "target_block_cpu_usage_pct": 2000,
            "max_transaction_cpu_usage": 150000,
            "min_transaction_cpu_usage": 100,
            "max_transaction_lifetime": 3600,
            "deferred_trx_expiration_window": 600,
            "max_transaction_delay": 3888000,
            "max_inline_action_size": 4096,
            "max_inline_action_depth": 4,
            "max_authority_depth": 6
          }
        },
        "hex_data": "0000100000000000e8030000000008000c000000f40100001400000064000000400d0300d0070000f049020064000000100e00005802000080533b000010000004000600"
      }
    ],
    "transaction_extensions": []
  }
}
```

现链上数据可以通过 `cleos get table eosio eosio global` 查看。

