# Governance

## 1. Text proposal commands:
### Parameter description:  

| Name                | Mark                                                           |
| :------             | :------                                                               |
| --title             | title of the proposal                                                        |
| --description       | description of the proposal (for text proposals only)                                      |
| --type              | type of the proposal initiated (for text proposals only)                                      |
| --deposit           | initial deposit specified when the proposal is initiated                                              |
| --from              | account name specified for sending a transaction                                                |
| --home              | account name and the directory where okchaincli is configured<br>if it is ~/.okchaincli can ignore the parameters |
| -b/--broadcast-mode | specific transaction broadcast modes (async, sync and block)                                 |

### Example:
```bash
okchaincli tx gov submit-text-proposal --title="test" --description="test" --type=Text --deposit="80okt" --from alice --home ~/.okchaincli -b block
```
### Successful response:
```
{
  "height": "156",
  "txhash": "86EB4B2B756E28A4553413DFDB7C0C5DBE2A61C46AE35A1970AF227263BE33F4",
  "data": "0102",
  "raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
  "logs": [
    {
      "msg_index": "0",
      "success": true,
      "log": ""
    }
  ],
  "tags": [
    {
      "key": "fee",
      "value": "0.01250000 okt"
    },
    {
      "key": "proposer",
      "value": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya"
    },
    {
      "key": "proposal-id",
      "value": "2"
    }
  ]
}
```
## 2. Parameter change proposal commands:
### Parameter description:

| Name                | Mark                                                                                                                                                                                                                                                             |
| :------             | :------                                                                                                                                                                                                                                                                 |
| --title             | title of the proposal                                                                                                                                                                                                                                                          |
| --type              | type of the proposal initiated (for ParameterChange proposals only)                                                                                                                                                                                                                             |
| --deposit           | initial deposit specified when the proposal is initiated                                                                                                                                                                                                                                                |
| --param             | specific parameters and values to be modified (gov/MinDeposit=1000okt<br>modify the MinDeposit parameters in the module to be governed to 1000okt. <br> Refer to the parameters that can be modified for each module [link](../../governance/parameter.html#id1) |
| --height            | block height when the specific parameter change proposal becomes effective (parameters to be modified changed to specific values), <br>the specific height must meet: higher than the current block height and lower than or equal to the sum of the current block height and [MaxBlockHeightPeriod](../../concepts/gov.html#id5)                                                                                                  |
| --from              | account name specified for sending a transaction                                                                                                                                                                                                                                                  |
| --home              | account name and the directory where okchaincli is configured<br>if it is ~/.okchaincli can ignore the parameters                                                                                                                                                                                                   |
| -b/--broadcast-mode | specific transaction broadcast modes (async, sync and block)                                                                                                                                                                                                                                  |

### Example:
```bash
okchaincli tx gov submit-param-change-proposal --title="Change gov/MinDeposit" --type="ParameterChange" --deposit="60okt" --from alice --param='gov/MinDeposit=1000okt' --height=1000 -b block
```
### Successful response:
```
{
  "height": "723",
  "txhash": "D24E9B7467325D8F77EEB3F9D8A34F27C6D1C2BB2BCA752FB0E2112A6119F2FB",
  "data": "0103",
  "raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
  "logs": [
    {
      "msg_index": "0",
      "success": true,
      "log": ""
    }
  ],
  "tags": [
    {
      "key": "fee",
      "value": "0.01250000 okt"
    },
    {
      "key": "proposer",
      "value": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya"
    },
    {
      "key": "proposal-id",
      "value": "3"
    },
    {
      "key": "param",
      "value": "[{\"subspace\":\"gov\",\"key\":\"MinDeposit\",\"value\":\"1000okt\"}]"
    }
  ]
}
```
## 3. DexList proposal commands:
### Parameter description:

| Name                | Mark                                                                                                                                                                                                    |
| :------             | :------                                                                                                                                                                                                        |
| --title             | title of the proposal                                                                                                                                                                                                 |
| --type              | type of the proposal initiated (for ParameterChange proposals only)                                                                                                                                                                    |
| --deposit           | initial deposit specified when the proposal is initiated                                                                                                                                                                                       |
| --listAsset         | specific token to be listed (you need to issue the token before listing, see [link](../../getting-start/command/token.html#id2)) for details                                                                                                                               |
| --quoteAsset        | specific token for the pair traded with listAsset (only support okt currently)                                                                                                                                                               |
| --initPrice         | initial price of the trading pair specified during listing as the reference price for the initial transaction                                                                                                                                                     |
| --maxPriceDigit     | precision of the price specified when placing an order (<= 8) <br> eg. if the value is 4, the specific price of the order cannot be a figure with more than 4 decimal places                                                                                                                                   |
| --maxSizeDigit      | precision of the quantity specified when placing an order (<= 8) <br> eg. if the value is 4, the specific quantity of the order cannot be a figure with more than 4 decimal places                                                                                                                                   |
| --minTradeSize      | quantity specified when placing an order cannot be lower than this value                                                                                                                                                                                   |
| --from              | account name specified for sending a transaction                                                                                                                                                                                         |
| --blockHeight       | effective block height for the specific listing proposal (for automatically activating the token listing) <br> If the proposal is approved and the token listing will be activated by [listing activation commands](../../getting-start/command/gov.html#id12), you do not need to specify the parameters <br> The specific height must meet: lower than or equal to the sum of the current block height and [MaxBlockHeight](../../concepts/gov.html#id5). If the specific value is 1000 but the block height is 1500 upon approval, the token listing will be immediately activated |
| --home              | account name and the directory where okchaincli is configured<br>if it is ~/.okchaincli can ignore the parameters                                                                                                                                          |
| -b/--broadcast-mode | specific transaction broadcast modes (async, sync and block)                                                                                                                                                                         |

### Example:
```bash
okchaincli tx gov submit-dex-list-proposal --title="list bcoin-7a4/okt" --type=DexList --deposit="1000okt"   --listAsset="bcoin-7a4" --quoteAsset="okt"  --initPrice="2500.25" --maxPriceDigit=4 --maxSizeDigit=4 --minTradeSize="0.001" --from alice --home=~/.okchaincli -b block
```
### Successful response:
```
{
  "height": "1048",
  "txhash": "AE4A6F4AAA42FEA80450B5F46CBA2C343FF5D5C8251BBC10ADD958100362BD39",
  "data": "0104",
  "raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
  "logs": [
    {
      "msg_index": "0",
      "success": true,
      "log": ""
    }
  ],
  "tags": [
    {
      "key": "fee",
      "value": "0.01250000 okt"
    },
    {
      "key": "proposer",
      "value": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya"
    },
    {
      "key": "proposal-id",
      "value": "4"
    }
  ]
}
```
## 4. Listing activation commands:
### Parameter description:

| Name                | Mark                                                           |
| :------             | :------                                                               |
| --proposal          | proposal id of DexList proposal specified to be activated                                    |
| --from              | account name specified for sending a transaction                                                |
| --home              | account name and the directory where okchaincli is configured<br>if it is ~/.okchaincli can ignore the parameters |
| -b/--broadcast-mode | specific transaction broadcast modes (async, sync and block)                                |

### Example:
```bash
okchaincli tx gov dexlist --proposal=4 --from alice --home ~/.okchaincli -b block
```
### Successful response:
```
{
  "height": "1685",
  "txhash": "7B67F9C6EB50EA02369167C68DF7DAE094F389324636E484D021D8ABE7935F6E",
  "raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
  "logs": [
    {
      "msg_index": "0",
      "success": true,
      "log": ""
    }
  ],
  "tags": [
    {
      "key": "fee",
      "value": "100000.01250000 okt"
    },
    {
      "key": "action",
      "value": "dex-list"
    },
    {
      "key": "list-asset",
      "value": "bcoin-a69"
    },
    {
      "key": "quote-asset",
      "value": "okt"
    },
    {
      "key": "init-price",
      "value": "2500.25000000"
    },
    {
      "key": "max-price-digit",
      "value": "4"
    },
    {
      "key": "max-size-digit",
      "value": "4"
    },
    {
      "key": "min-trade-size",
      "value": "0.00100000"
    }
  ]
}
```
## 5. Version upgrade proposal commands:
Please refer to [link](/governance/upgrade/)
## 6. Proposal deposit commands:
### Example:
Deposit the specific proposal through proposal id
```bash
okchaincli tx gov deposit 1 500okt --from alice --home ~/.okchaincli/ -b block
```
### Successful response:
```
{
  "height": "1328",
  "txhash": "FBFB981D1B5CD1C4FDE2A60D3EA1CB5C5F7E8DDF7AA54CCA325B8896E990C46A",
  "raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
  "logs": [
    {
      "msg_index": "0",
      "success": true,
      "log": ""
    }
  ],
  "tags": [
    {
      "key": "fee",
      "value": "0.01250000 okt"
    },
    {
      "key": "depositor",
      "value": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya"
    },
    {
      "key": "proposal-id",
      "value": "4"
    },
    {
      "key": "voting-period-start",
      "value": "4"
    }
  ]
}
```
## 7. Proposal voting commands:
### Example:
Vote for the specific proposal through proposal id (Yes, No, Abstain or NoWithVeto)

```bash
okchaincli tx gov vote 2 Yes --from alice --home ~/.okchaincli/ -b block
```
### Successful response:
```
{
  "height": "1550",
  "txhash": "7E62A12E93FFBA280E814D4DE3627FD1015C8B711EBAB6A4C202232B338526F6",
  "raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
  "logs": [
    {
      "msg_index": "0",
      "success": true,
      "log": ""
    }
  ],
  "tags": [
    {
      "key": "fee",
      "value": "0.01250000 okt"
    },
    {
      "key": "voter",
      "value": "okchain1svzxp4ts5le2s4zugx34ajt6shz2hg42p0e6tw"
    },
    {
      "key": "proposal-id",
      "value": "4"
    },
    {
      "key": "proposal-status",
      "value": "Passed"
    }
  ]
}
```
## 8. Proposal query commands:
### Query specific proposals:
#### Example:
Query the proposal through proposal id
```bash
okchaincli query gov proposal 4 --home ~/.okchaincli/
```
#### Successful response:
```
{
  "type": "gov/DexListProposal",
  "value": {
    "BasicProposal": {
      "proposal_id": "4",
      "title": "list bcoin-7a4/okt",
      "description": "",
      "proposal_type": "DexList",
      "proposal_status": "Passed",
      "tally_result": {
        "yes": "100000000",
        "abstain": "0",
        "no": "0",
        "no_with_veto": "0"
      },
      "submit_time": "2019-07-29T03:25:36.759218374Z",
      "deposit_end_time": "2019-07-30T03:25:36.759218374Z",
      "total_deposit": [
        {
          "denom": "okt",
          "amount": "21000.00000000"
        }
      ],
      "voting_start_time": "2019-07-29T03:31:43.90917706Z",
      "voting_end_time": "2019-08-01T03:31:43.90917706Z"
    },
    "proposer": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya",
    "list_asset": "bcoin-a69",
    "quote_asset": "okt",
    "init_price": "2500.25000000",
    "block_height": "0",
    "max_price_digit": "4",
    "max_size_digit": "4",
    "min_trade_size": "0.001",
    "dex_list_start_time": "2019-07-29T03:36:57.647117542Z",
    "dex_list_end_time": "2019-07-30T03:36:57.647117542Z"
  }
}
```
### Query all proposals:
#### Example:
```bash
okchaincli query gov proposals --home ~/.okchaincli/
```
#### Successful response:
```
[
  {
    "type": "gov/TextProposal",
    "value": {
      "BasicProposal": {
        "proposal_id": "1",
        "title": "test",
        "description": "test",
        "proposal_type": "Text",
        "proposal_status": "DepositPeriod",
        "tally_result": {
          "yes": "0",
          "abstain": "0",
          "no": "0",
          "no_with_veto": "0"
        },
        "submit_time": "2019-07-29T03:03:41.765548835Z",
        "deposit_end_time": "2019-07-30T03:03:41.765548835Z",
        "total_deposit": [
          {
            "denom": "okt",
            "amount": "80.00000000"
          }
        ],
        "voting_start_time": "0001-01-01T00:00:00Z",
        "voting_end_time": "0001-01-01T00:00:00Z"
      }
    }
  },
  {
    "type": "gov/TextProposal",
    "value": {
      "BasicProposal": {
        "proposal_id": "2",
        "title": "test",
        "description": "test",
        "proposal_type": "Text",
        "proposal_status": "DepositPeriod",
        "tally_result": {
          "yes": "0",
          "abstain": "0",
          "no": "0",
          "no_with_veto": "0"
        },
        "submit_time": "2019-07-29T03:05:59.446787436Z",
        "deposit_end_time": "2019-07-30T03:05:59.446787436Z",
        "total_deposit": [
          {
            "denom": "okt",
            "amount": "80.00000000"
          }
        ],
        "voting_start_time": "0001-01-01T00:00:00Z",
        "voting_end_time": "0001-01-01T00:00:00Z"
      }
    }
  },
  {
    "type": "gov/ParameterProposal",
    "value": {
      "BasicProposal": {
        "proposal_id": "3",
        "title": "Change gov/MinDeposit",
        "description": "",
        "proposal_type": "ParameterChange",
        "proposal_status": "DepositPeriod",
        "tally_result": {
          "yes": "0",
          "abstain": "0",
          "no": "0",
          "no_with_veto": "0"
        },
        "submit_time": "2019-07-29T03:18:21.761155019Z",
        "deposit_end_time": "2019-07-30T03:18:21.761155019Z",
        "total_deposit": [
          {
            "denom": "okt",
            "amount": "60.00000000"
          }
        ],
        "voting_start_time": "0001-01-01T00:00:00Z",
        "voting_end_time": "0001-01-01T00:00:00Z"
      },
      "params": [
        {
          "subspace": "gov",
          "key": "MinDeposit",
          "value": "1000okt"
        }
      ],
      "height": "1000"
    }
  }
]
```
### Query governance parameters:
#### Example:
```bash
okchaincli query gov params --home ~/.okchaincli/
```
#### Successful response:
```
{
  "max_deposit_period": "86400000000000",
  "min_deposit": [
    {
      "denom": "okt",
      "amount": "100.00000000"
    }
  ],
  "voting_period": "259200000000000",
  "dex_list_max_deposit_period": "86400000000000",
  "dex_list_min_deposit": [
    {
      "denom": "okt",
      "amount": "20000.00000000"
    }
  ],
  "dex_list_voting_period": "259200000000000",
  "dex_list_vote_fee": [
    {
      "denom": "okt",
      "amount": "0.00000000"
    }
  ],
  "dex_list_max_block_height": "10000",
  "dex_list_fee": [
    {
      "denom": "okt",
      "amount": "100000.00000000"
    }
  ],
  "dex_list_expire_time": "86400000000000",
  "quorum": "0.33400000",
  "threshold": "0.50000000",
  "veto": "0.33400000",
  "max_block_height_period": "100000",
  "max_tx_num_per_block": "2000"
}
```
#### Query governance parameters:

| Parameters              | Mark                                                                                               |
| :----                   | :----                                                                                                      |
| MaxDepositPeriod        | Text/ParameterChange/deposit period for app upgrade proposal                                                                       |
| MinDeposit              | Text/ParameterChange/deposit limit for app upgrade proposal<br>if the proposal deposit exceeds this value, the Voting Period will be effective                               |
| VotingPeriod            | Text/ParameterChange/voting period for app upgrade proposal                                                                         |
| DexListMaxDepositPeriod | deposit period for DexList proposal                                                                                      |
| DexListMinDeposit       | deposit limit for DexList proposal                                                                                      |
| DexListVotingPeriod     | voting period for DexList proposal                                                                                       |
| DexListVoteFee          | fees charged for accounts voting Yes/NoWithVeto on DexList proposal according to <br> the staking weight of DexListVoteFee* accounts |
| DexListMaxBlockHeight   | block height specified for automatically activating the token listing does not exceed the sum of the current block height and DexListMaxBlockHeight                                            |
| DexListFee              | fees for listing activation                                                                                            |
| DexListExpireTime       | validity period of listing activation upon approval of DexList proposal                                                                           |
| Quorum                  | weight threshold for voting on the entire network used for [voting statistics](../../concepts/gov.html#id4)                                                                                     |
| Threshold               | weight threshold for the proportion of Yes votes to all non-abstained votes used for [voting statistics](../../concepts/gov.html#id4)                                                                        |
| Veto                    | weight threshold for the proportion of NoWithVeto votes to all votes used for [voting statistics](../../concepts/gov.html#id4)                                                                       |
| MaxBlockHeightPeriod    | parameter change proposal specifies that the automatically effective block height does not exceed the sum of the current block height and MaxBlockHeightPeriod                                     |
| MaxTxNumPerBlock        | maximum number of transactions contained in each block                                                                                 |

