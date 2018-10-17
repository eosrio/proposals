## Motivation

Since the mainnet launch the global blockchain parameters were left as default, and now with a recent increase of the usage, the users noticed that the system contract is triggering the CPU congestion mode too early. As soon as a block hits 10% of the total 200ms of CPU time allowed per block, the CPU allocation algorithm switches to the congestion mode and every user is left with his share of the remaining allocation based on their stake in proportion to the whole network stake. What ended up happening is that while the actual CPU usage of the validators is very low, the CPU price became higher.

This proposal aims to change the current value for `target_block_cpu_usage_pct` from `1000` (10%) to `2000` (20%), tests were performed on the CryptoKylin testnet showing that the algorithm transition happens in a much smoother way and also allowed more resources from the nodes to be used. Test reports are available here: 

https://docs.google.com/spreadsheets/d/1m_YZ1FFC1awRjXEA-wjtXAl7LzyWB9xE3qupdlQU7fc/edit?usp=sharing

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

https://docs.google.com/spreadsheets/d/1m_YZ1FFC1awRjXEA-wjtXAl7LzyWB9xE3qupdlQU7fc/edit?usp=sharing

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


# 한국어 번역 (by EOSYS)

## 동기

메인넷 출시 이후 글로벌 블록체인 파라미터는 디폴트값으로 남았으며, 최근에는 사용량이 증가하면서 사용자는 시스템 컨트랙트으로 인해 CPU 정체 정체 현상을 이른 시점에 경험하게 되었습니다. 블록 당 허용되는 CPU 시간의 총 200ms 중 10 %에 도달하면 CPU 할당 알고리즘은 혼잡(congestion) 모드로 전환되며, 모든 사용자는 전체 네트워크에 비례하여 스테이크된 EOS양을 기반으로 나머지 할당량을 공유합니다. 결과적으로 검증자(validator)의 실제 CPU 사용량은 매우 낮지만 CPU 가격은 높아졌습니다.

이 제안은 `target_block_cpu_usage_pct`의 현재 값을 `1000`(10 %)에서 `2000`(20 %)으로 변경하는 것을 목표로 하고 있으며, CryptoKylin 테스트넷에서 진행한 테스트를 통해 네트워크에서 알고리즘 전환이 훨씬 원활하게 발생하고 노드에서 더 많은 리소스를 사용할 수 있음을 보여줌을 확인했습니다. 테스트 보고서는 다음에서 확인할 수 있습니다.

https://docs.google.com/spreadsheets/d/1m_YZ1FFC1awRjXEA-wjtXAl7LzyWB9xE3qupdlQU7fc/edit?usp=sharing

이상적으로, 이 값은 메인넷의 사용량 증가를 고려하여 업데이트 되어야 하며 언제든지 되돌릴 수 있는 안전한 파라미터입니다.

## 제안 리뷰

유일한 액션은 eosio::setparams이며, 이는 `cleos multisig review eosriobrazil updateparams`를 통해 쉽게 확인할 수 있으며, 다음과 같은 값을 리턴합니다:

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

체인 위의 값은 usign `cleos get table eosio eosio global` 를 통해 되돌릴 수 있으며, 시스템 컨트랙트를 통해 확장할 수 있는 더 많은 파라미터들이 있습니다. 따라서 setparams 액션을 통과할 필요가 없습니다.
