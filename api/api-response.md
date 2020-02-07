---
description: Learn about Totle's API response parameters here.
---

# API Response

The responses of the `swap` and `pay` endpoints are built in an easily understood format with the following sections:

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
| Parameter | Description |
| :--- | :--- |
| summary | user-readable details of all the possible swap orders found \(including the best-possible trading pair and the alternative options\) |
| sourceAsset | information about the token being sold |
| address | the token contract address |
| symbol | the token symbol |
| decimals | the number of decimals assigned to the token |
| sourceAmount | the amount of token being sold |
| destinationAsset | information about the token being purchased |
| destinationAmount | the amount of token being received |
| runnerUpRoutes | routes considered by Totle that are not chosen for execution due to |
| trades | the individual trades that make up the route taken to swap one token to another |
| orders | the transaction\(s\) needed to fill a trade \(e.g. trading Token A to Token B may require two or more orders\) |
| exchange | the exchange on which the swap occurs |
| id | the ID used by Totle to identify the exchange |
| name | the name of the exchange |
| fee | information about the fee assessed by the exchange facilitating the transaction |
| percentage | the fee amount as a percentage of the transaction |
| amount | the fee amount |
| asset | information about the token type used to pay the assessed fee |
| runnerUpOrders | orders considered by Totle that are not chosen for execution due to sub-optimal rates |
| totleFee | information about the fee assessed by Totle for facilitating the transaction |
| partnerFee | information about the fee assessed by third-party partners who deploy a partner contract on Totle's platform |
| transactions | information about the transaction to be submitted |
| type | the type of transaction to be performed \(e.g., `trade`\) |
| tx | full transaction object to be signed and included in your wallet |
| to | contract address to which the token is sent |
| from | the user's wallet address from which the token originates |
| value | the value of the token sent |
| data | encoded payload the contract needs to execute the trades |
| gas | suggested gas price for the provided payload |
| gasLimit | maximum gas limit for the payload provided |
| nonce | the user's wallet transaction count required in every transaction |
| rateLimit | rate limit information |
| callsMade | the number of calls you have made |
| callsLeft | the number of calls you can make before hitting a rate limit |
| signature | the signed payload that verifies the payload originates from Totle |
| expiration | information about when the returned payload expires and is no longer valid |
| blockNumber | the block number in which the returned payload is no longer valid |
| estimatedTimeSpan | the estimated timestamp \(in seconds\) when `blockNumber` is reached |
{% endtab %}
{% endtabs %}

