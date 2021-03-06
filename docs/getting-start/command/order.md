# Tx orders

Order attributes

|      Name       |      Type       |       Mark        |
| :-------------: | :-------------: | :------------------: |
| txHash          |string           | txHash of the place order tx|
| orderId         |string           | order id, denoted as "blockHeight-orderNumInBlock".|
| sender          |string           | order maker address|
| product         |string           | product for trading pair in full name of the tokens|
| side            |string           | BUY/SELL|
| price           |string           | price of the order|
| quantity        |string           | quantity of the order|
| status          |int64            | order status,(0-5) respectively represents (Open, Filled, Cancelled, Expired, PartialFilledCancelled, PartialFilledExpired)|
| filledAvgPrice  |string           | filled average price|
| remainQuantity  |string           | Remaining quantity of the order|
| remainLocked    |string           | Remaining locked quantity of token|
| timestamp       |int64            | created timestamp|
| extraInfo       |string           | extra info of order in json format|

## 1. Place or cancel an order:

Dex supports order placing and cancellation functions. Commands are as follows:

```bash
okchaincli tx order
```

Secondary sub-commands mainly include the following 2 functions

### 1.1 Place an order:
#### Example:
Create a new limit order
```bash
# place an order
okchaincli tx order new [product] [side] [price] [quantity]
```
```
Flags:
  -a, --account-number uint     The account number of the signing account (offline mode only)
  -b, --broadcast-mode string   Transaction broadcasting mode (sync|async|block) (default "sync")
      --dry-run                 ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it
      --fees string             Fees to pay along with transaction; eg: 10uatom
      --from string             Name or address of private key with which to sign
      --gas string              gas limit to set per-transaction; set to "auto" to calculate required gas automatically (default 999999990000) (default "999999990000")
      --gas-adjustment float    adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored  (default 1)
      --gas-prices string       Gas prices to determine the transaction fee (e.g. 10uatom)
      --generate-only           Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase is not accessible)
  -h, --help                    help for new
      --indent                  Add indent to JSON response
      --ledger                  Use a connected Ledger device
      --memo string             Memo to send along with transaction
      --node string             <host>:<port> to tendermint rpc interface for this chain (default "tcp://localhost:26657")
      --print-response          return tx response (only works with async = false) (default true)
      --sequence uint           The sequence number of the signing account (offline mode only)
      --trust-node              Trust connected full node (don't verify proofs for responses) (default true)
  -y, --yes                     Skip tx broadcasting prompt confirmation

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
      --home string       directory for config and data (default "/Users/dwil/.okchaincli")
  -o, --output string     Output format (text|json) (default "text")
      --passwd string     Pass word of sender (default "12345678")
      --trace             print out full stack trace on errors
```
#### Successful response:
```
# example
okchaincli tx order new mycoin_okt BUY 9.9 2.0 --from alice
# example return
{
  "txhash": "57A390CBBE43548F112956DF6CA7146E14A02720F2895908B3A057136CE0324D"
}
```
`product`indicates the name of a trading pair

`side`indicates buy or sell, BUY/SELL value

`price`indicates price

`quantity`indicates buy or sell quantity


### 1.2 Cancel an order:
#### Example:
```bash
okchaincli tx order cancel [orderId]
```
```
Flags:
  -a, --account-number uint     The account number of the signing account (offline mode only)
  -b, --broadcast-mode string   Transaction broadcasting mode (sync|async|block) (default "sync")
      --dry-run                 ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it
      --fees string             Fees to pay along with transaction; eg: 10uatom
      --from string             Name or address of private key with which to sign
      --gas string              gas limit to set per-transaction; set to "auto" to calculate required gas automatically (default 999999990000) (default "999999990000")
      --gas-adjustment float    adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored  (default 1)
      --gas-prices string       Gas prices to determine the transaction fee (e.g. 10uatom)
      --generate-only           Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase is not accessible)
  -h, --help                    help for cancel
      --indent                  Add indent to JSON response
      --ledger                  Use a connected Ledger device
      --memo string             Memo to send along with transaction
      --node string             <host>:<port> to tendermint rpc interface for this chain (default "tcp://localhost:26657")
      --print-response          return tx response (only works with async = false) (default true)
      --sequence uint           The sequence number of the signing account (offline mode only)
      --trust-node              Trust connected full node (don't verify proofs for responses) (default true)
  -y, --yes                     Skip tx broadcasting prompt confirmation

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|bcoin) (default "hex")
      --home string       directory for config and data (default "/Users/dwil/.okchaincli")
  -o, --output string     Output format (text|json) (default "text")
      --passwd string     Pass word of sender (default "12345678")
      --trace             print out full stack trace on errors
```
#### Successful response:
```
# example
okchaincli tx order cancel ID0000000054-0000 --from alice 

# example return
{
  "txhash": "57A390CBBE43548F112956DF6CA7146E14A02720F2895908B3A057136CE0324D"
}
```
`orderId` indicates order id, which is the only id automatically generated on the application layer

## 2. Operation query:

Dex supports various functions including order query, depthbook and users' order books. Commands are as follows:

```bash
okchaincli query order
```

Secondary sub-commands mainly include the following functions
### 2.1 Order details:
#### Example:
```bash
okchaincli query order detail [orderId]
```
```
Flags:
  -h, --help          help for detail
      --indent        Add indent to JSON response
      --ledger        Use a connected Ledger device
      --node string   <host>:<port> to tendermint rpc interface for this chain (default "tcp://localhost:26657")
      --trust-node    Trust connected full node (don't verify proofs for responses)

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|bcoin) (default "hex")
      --home string       directory for config and data (default "/Users/dwil/.okchaincli")
  -o, --output string     Output format (text|json) (default "text")
      --passwd string     Pass word of sender (default "12345678")
      --trace             print out full stack trace on errors
```
#### Successful response:
```
# example
okchaincli query order detail ID0000000007-0000
# example return
{
 "txHash": "CF8CEC36B97F089DEA243655A70D1CB2AE906D712D71210BCDEBC47F184DB6C2",
 "orderId": "ID0000000007-0000",
 "sender": "cosmos1cwvqt96wj222k2hue4pxcy5nxch6maaklknn7p",
 "product": "mycoin_okt",
 "side": "BUY",
 "price": "10.000000000000000000",
 "quantity": "1.100000000000000000",
 "status": "0",
 "filledAvgPrice": "10.000000000000000000",
 "remainQuantity": "0.100000000000000000",
 "timestamp": "1554273977"
}
```
### 2.2 Order depthbook:
#### Example:
```bash
okchaincli query order depthbook [product]
```
```
Flags:
  -h, --help          help for depthbook
      --indent        Add indent to JSON response
      --ledger        Use a connected Ledger device
      --node string   <host>:<port> to tendermint rpc interface for this chain (default "tcp://localhost:26657")
      --size int      depth book single-side size (default 200)
      --trust-node    Trust connected full node (don't verify proofs for responses)

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|bcoin) (default "hex")
      --home string       directory for config and data (default "/Users/dwil/.okchaincli")
  -o, --output string     Output format (text|json) (default "text")
      --passwd string     Pass word of sender (default "12345678")
      --trace             print out full stack trace on errors
```
#### Successful response:
```
# example
okchaincli query order depthbook mycoin_okt
# example return
{
 "code": "0",
 "msg": "",
 "asks": [
  {
   "price": "10.100000000000000000",
   "quantity": "1.000000000000000000"
  }
 ],
 "bids": [
  {
   "price": "10.000000000000000000",
   "quantity": "0.100000000000000000"
  },
  {
   "price": "9.900000000000000000",
   "quantity": "2.000000000000000000"
  },
  {
   "price": "9.800000000000000000",
   "quantity": "10.000000000000000000"
  }
 ]
}
```
### 2.3 Query storage information of order modules:
#### Example:
```bash
okchaincli query order store
```
```
Flags:
      --dbpath string   db path (if this path is given, query through local file)
      --dump            dump all key-value constants of specified module
  -h, --help            help for store
      --indent          Add indent to JSON response
      --ledger          Use a connected Ledger device
      --node string     <host>:<port> to tendermint rpc interface for this chain (default "tcp://localhost:26657")
      --trust-node      Trust connected full node (don't verify proofs for responses)

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|bcoin) (default "hex")
      --home string       directory for config and data (default "/Users/dwil/.okchaincli")
  -o, --output string     Output format (text|json) (default "text")
      --passwd string     Pass word of sender (default "12345678")
      --trace             print out full stack trace on errors
```
#### Successful response:
```
# example
okchaincli query order store

# example return
{
	"StoreOrderNum": "1",
	"DepthBookNum": {
		"mycoin_okt": "1"
	},
	"BookOrderIdsNum": {
		"bookitem:mycoin_okt:11.10000000:SELL": "1"
	}
}

```
### 2.4 Query all parameters during governance:
#### Example:
```bash
okchaincli query order params
```
```
Flags:
  -h, --help          help for params
      --indent        Add indent to JSON response
      --ledger        Use a connected Ledger device
      --node string   <host>:<port> to tendermint rpc interface for this chain (default "tcp://localhost:26657")
      --trust-node    Trust connected full node (don't verify proofs for responses)

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|bcoin) (default "hex")
      --home string       directory for config and data (default "/Users/dwil/.okchaincli")
  -o, --output string     Output format (text|json) (default "text")
      --passwd string     Pass word of sender (default "12345678")
      --trace             print out full stack trace on errors
```
#### Successful response:
```
# example
okchaincli query order params

# example return
{
  "order_expire_blocks": "86400",
  "max_deals_per_block": "2000",
  "new_order": "0.00000000",
  "cancel": "0.01000000",
  "cancel_native": "0.00200000",
  "expire": "0.01000000",
  "expire_native": "0.00200000",
  "trade_fee_rate": "0.00100000",
  "trade_fee_rate_native": "0.00040000"
}
```
