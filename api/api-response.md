---
description: Learn about Totle's API response parameters here.
---

# API Response

The response of the `swap` endpoint is built in an easily understood format with the following sections:

## Summary

The summary is a comprehensive breakdown of the transaction where you can get information about the trades, orders, exchanges, fees, etc. in a human readable format.

## Transactions

The transactions section is a list of complete transaction objects that the end user must sign and submit to the Ethereum blockchain. Approval transactions will be prepended to the array. Sign and submit the transactions as they are ordered in the array. 

{% hint style="warning" %}
Modification of the transaction objects is strongly discouraged
{% endhint %}

## Expiration

The expiration section contains the expiration block and the estimated expiration timestamp of the Totle swap. Expired transactions will be reverted by the smart contract.

{% tabs %}
{% tab title="JSON" %}
```javascript
{
    "success": true,
    "response": {
        "id": "0x46d0648312ee4fb099117b9f9d18767ab7fcd94fde5240e59b72118a7338609e",
        "summary": [
            {
                "sourceAsset": {
                    "address": "0x0000000000000000000000000000000000000000",
                    "symbol": "ETH",
                    "decimals": "18"
                },
                "sourceAmount": "1000000000000000000",
                "destinationAsset": {
                    "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
                    "symbol": "DAI",
                    "decimals": "18"
                },
                "destinationAmount": "219849000000000000000",
                "notes": [],
                "rate": "219.849",
                "guaranteedRate": "198.84900000000000021",
                "market": {
                    "rate": "219.84900000000000021",
                    "slippage": "0.000000000000000096%"
                },
                "runnerUpRoutes": [
                    {
                        "baseAsset": {
                            "address": "0x89d24a6b4ccb1b6faa2625fe562bdd9a23260359",
                            "symbol": "SAI",
                            "decimals": "18"
                        },
                        "sourceAsset": {
                            "address": "0x0000000000000000000000000000000000000000",
                            "symbol": "ETH",
                            "decimals": "18"
                        },
                        "sourceAmount": "1000000000000000000",
                        "destinationAsset": {
                            "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
                            "symbol": "DAI",
                            "decimals": "18"
                        },
                        "destinationAmount": "211769682759420945040"
                    }
                ],
                "trades": [
                    {
                        "sourceAsset": {
                            "address": "0x0000000000000000000000000000000000000000",
                            "symbol": "ETH",
                            "decimals": "18"
                        },
                        "sourceAmount": "1000000000000000000",
                        "destinationAsset": {
                            "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
                            "symbol": "DAI",
                            "decimals": "18"
                        },
                        "destinationAmount": "219849000000000000000",
                        "orders": [
                            {
                                "sourceAsset": {
                                    "address": "0x0000000000000000000000000000000000000000",
                                    "symbol": "ETH",
                                    "decimals": "18"
                                },
                                "sourceAmount": "1000000000000000000",
                                "destinationAsset": {
                                    "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
                                    "symbol": "DAI",
                                    "decimals": "18"
                                },
                                "destinationAmount": "220400000000000000000",
                                "exchange": {
                                    "id": 19,
                                    "name": "PMM"
                                },
                                "fee": {
                                    "percentage": "0",
                                    "amount": "0",
                                    "asset": {
                                        "address": "0x0000000000000000000000000000000000000000",
                                        "symbol": "ETH",
                                        "decimals": "18"
                                    }
                                }
                            }
                        ],
                        "runnerUpOrders": [
                            {
                                "sourceAsset": {
                                    "address": "0x0000000000000000000000000000000000000000",
                                    "symbol": "ETH",
                                    "decimals": "18"
                                },
                                "sourceAmount": "5449375978333281110",
                                "destinationAsset": {
                                    "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
                                    "symbol": "DAI",
                                    "decimals": "18"
                                },
                                "destinationAmount": "1199999999999999999967",
                                "exchange": {
                                    "id": 22,
                                    "name": "0x V3"
                                },
                                "fee": {
                                    "percentage": "0",
                                    "amount": "0",
                                    "asset": {
                                        "address": "0xe41d2489571d322189246dafa5ebde1f4699f498",
                                        "symbol": "ZRX",
                                        "decimals": "18"
                                    }
                                }
                            }
                        ]
                    }
                ],
                "totleFee": {
                    "asset": {
                        "address": "0x0000000000000000000000000000000000000000",
                        "symbol": "ETH",
                        "decimals": "18"
                    },
                    "percentage": "0.25",
                    "amount": "2506265664160401"
                },
                "partnerFee": {
                    "asset": {
                        "address": "0x0000000000000000000000000000000000000000",
                        "symbol": "ETH",
                        "decimals": "18"
                    },
                    "percentage": "0",
                    "amount": "0"
                }
            }
        ],
        "transactions": [
            {
                "type": "swap",
                "tx": {
                    "to": "0x3b21d6d25e7f036c8277efe9a7ebf17ca12fe4f6",
                    "from": "0x0000000000000000000000000000000000000000",
                    "value": "1000000000000000000",
                    "data": "0x5f10dffc00000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000100000000000000000000000000d53799e6f0728fdfb56b746dcd7b75dfcb422d7400000000000000000000000000000000000000000000000000000000008ffd0f46d0648312ee4fb099117b9f9d18767ab7fcd94fde5240e59b72118a7338609e00000000000000000000000000000000000000000000000000000002540be400000000000000000000000000000000000000000000000000000000000000001c1562529900b977538f0ee87551c95cd0204ac0baeecf522e5d31caeb2403b2a61c99f9dc6b89210dbf22ebc78e63ab802ea04aa7f01ed914df6173dd75694f8700000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000b8f7cbbab5c1ba00000000000000000000000000000000000000000000000000ab9ea7e9efe5e40000000000000000000000000000000000000000000000000000de0b6b3a764000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000000000000000000000000000006b175474e89094c44da98b954eedeac495271d0f0000000000000000000000000000000000000000000000000de0b6b3a7640000000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000a00000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000003a00000000000000000000000009c119a139b9edcdb65b534c5c36d15d88bda8f4200000000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000000000000300000000000000000000000000000000000000000000000000000000000000002000000000000000000000000056178a0d5f301baf6cf3e1cd53d9863437345bf90000000000000000000000009c119a139b9edcdb65b534c5c36d15d88bda8f4200000000000000000000000055662e225a3376759c24331a9aed764f8f0c9fbb000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000bf2aa1845501800000000000000000000000000000000000000000000000000000de0b6b3a764000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000005e3d863800000000000000000000000000000000000000000000000015f1292b6f0ee11b00000000000000000000000000000000000000000000000000000000000001a0000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000002600000000000000000000000000000000000000000000000000000000000000024f47261b00000000000000000000000006b175474e89094c44da98b954eedeac495271d0f000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000024f47261b0000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc20000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000421bdf4bceee295e4f6b24467c5850290faba16e66061112c931008b09e0c6e04c4f425bf35e7364d18243d91a5392b59146d2c2e9e715f67e3a7c0aecfdce37376a030000000000000000000000000000000000000000000000000000000000000000000000000000000000002e49cab231386478c56173b744ea428f6edc94a6000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000003800000000000000000000000000000000000000000000000000000000000000020000000000000000000000000b0dd0dcada73b715e3b5567ab17bd7f37216a6370000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000410d586a20a4bfffdf0000000000000000000000000000000000000000000000004ba012948c1a1b5600000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000005e3d8649000000000000000000000000000000000000000000000000000001702050e3aa00000000000000000000000000000000000000000000000000000000000001e0000000000000000000000000000000000000000000000000000000000000024000000000000000000000000000000000000000000000000000000000000002a000000000000000000000000000000000000000000000000000000000000002c000000000000000000000000000000000000000000000000000000000000002e00000000000000000000000000000000000000000000000000000000000000024f47261b00000000000000000000000006b175474e89094c44da98b954eedeac495271d0f000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000024f47261b0000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc2000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000421cc4ee3d83de446dbd8eaf0ed7cf528c38ffe70cbc0170e906c7ae2271d5557a2e518c658895156b9eb853f30fc149c1cfeb7f4324286def67641fca54221c5d1703000000000000000000000000000000000000000000000000000000000000",
                    "gasPrice": "10000000000",
                    "gas": "1000000"
                }
            }
        ],
        "expiration": {
            "blockNumber": 9436431,
            "estimatedTimestamp": 1581090812
        }
    }
}
```
{% endtab %}

{% tab title="Parameters List" %}
## Common Parameter Objects

### `Token Details`

| Parameter | Description |
| :--- | :--- |
| address | Address of the token |
| symbol | Symbol of the token |
| decimals | Number of decimals the token has |

### `Fee Details`

| Parameter | Description |
| :--- | :--- |
| percentage | The percentage being used to calculate the fee amount |
| amount | The fee amount denoted in the `fee.asset` token |
| asset | `Token Details` of the token which the fee is denoted in |

### `Token Amount Details`

| Parameter | Description |
| :--- | :--- |
| sourceAsset | `Token Details` of the token being sold |
| sourceAmount | Amount of the token being sold |
| destinationAsset | `Token Details` of the token being bought |
| destinationAmount | Amount of the token being bought |

### `Route Details` extends `Token Amount Details`

| Parameter | Description |
| :--- | :--- |
| baseAsset? | `Token Details` of the token used for a middle trade between `sourceAsset` and `destinationAsset` |

### `Trade Details` extends `Token Amount Details`

| Parameter | Description |
| :--- | :--- |
| orders\[\] | Array of `Order Details` for the main orders that were selected |
| runnerUpOrders\[\] | Array of `Order Details` for the backup orders that were selected to be used if any of the main orders fail |

### `Order Details` extends `Token Amount Details`

| Parameter | Description  |
| :--- | :--- |
| exchange | Details of the exchange the order is for |
| exchange.id | Id of the order's exchange. List of exchanges can be found [here](https://api.totle.com/exchanges) |
| exchange.name | Name of the order's exchange |
| fee | `Fee Details` of the fees taken by the exchange |

## API Parameters

| Parameter | Description |
| :--- | :--- |
| success | Whether or not the API request was successful |
| response | The object that contains the response details |
| response.id | Unique identifier for this request/response pair |
| response.summary\[\] | Array of human-readable details of the requested swaps' best route. Contains information in `Route Details` |
| response.summary\[\].notes\[\] | Array of strings of any extra details  |
| response.summary\[\].rate | The rate of this swap denoted in `(destinationAmount / (10 ** destinationAsset.decimals)) / (sourceAmount / (10 ** sourceAsset.decimals))` |
| response.summary\[\].guaranteedRate | Rate that is guaranteed based of the supplied `maxMarketSlippagePercent` |
| response.summary\[\].runnerUpRoutes\[\] | Array of `Route Details` considered by Totle that were not chosen for execution  |
| response.summary\[\].trades\[\] | Array of `Trade Details` that make up the route  |
| response.summary\[\].totleFee | `Fee Details` of the fee taken by Totle for facilitating the transaction |
| response.summary\[\].partnerFee | `Fee Details` of the fee taken by third-party partners who deploy a partner contract on Totle's platform |
| response.transactions\[\] | Array of transaction objects auto-generated to perform the swaps described above in the summary. If multiple transaction objects are returned, the ones preceding the `swap` transaction will be `token approval` transactions |
| response.transactions\[\].type | The type of transaction to be performed \(e.g., `swap` or `approval`\) |
| response.transactions\[\].tx | A full auto-generated transaction object to be signed and submitted on-chain |
| response.transactions\[\].tx.to | Contract address to which the transaction is sent to |
| response.transactions\[\].tx.from | The user's wallet address from which the transaction will originate |
| response.transactions\[\].tx.value | The Ether value to be included in the transaction |
| response.transactions\[\].tx.data | The encoded payload data the contract needs to execute the swaps |
| response.transactions\[\].tx.gas | The suggested gas price for the transaction payload \(users are strongly discouraged to modify this value\) |
| response.transactions\[\].tx.gasLimit | The maximum gas limit for the transaction \(users are strongly discouraged to modify this value\) |
| response.transactions\[\].tx.nonce | The user's wallet transaction count required in every transaction |
| response.expiration | Information about when the returned payload expires and is no longer valid |
| response.expiration.blockNumber | The block number in which the returned payload is no longer valid |
| response.expiration.estimatedTimestamp | The estimated timestamp \(in seconds\) when `blockNumber` is reached |
{% endtab %}
{% endtabs %}

