---
description: Learn about Totle's API response parameters here.
---

# API Response

The payload returned by the `swap` and `pay` endpoints is optimized for Smart Contracts and is not easily read by end users. However, all endpoints return a human-readable summary of the trades that will be executed as part of the transaction. This is helpful to those who wish to review the transaction before signing it. The summary uses JSON formatting:

{% tabs %}
{% tab title="JSON" %}
```javascript
"summary": [
  {
    "baseAsset": {
      "address": "0x0...00",
      "symbol": "ETH",
      "decimals": "18"
    },
    "sourceAsset": {
      "address": "0x0...7ef",
      "symbol": "BAT",
      "decimals": "18"
    },
    "sourceAmount": "100000000000000000",
    "destinationAsset": {
      "address": "0x0...7ef",
      "symbol": "BAT",
      "decimals": "18"
    },
    "destinationAmount": "100108060297981726",
    "notes": [],
    "rate": "1.00108060297981726",
    "market": {
      "rate": "1.00108060297981726",
      "slippage": "0%"
    },
    "runnerUpRoutes": [
      {
        "sourceAsset": {
          "address": "0x0...7ef",
          "symbol": "BAT",
          "decimals": "18"
        },
        "sourceAmount": "100000000000000000",
        "destinationAsset": {
          "address": "0x0...7ef",
          "symbol": "BAT",
          "decimals": "18"
        },
        "destinationAmount": "99657574026640315"
      }
    ],
    "trades": [
      {
        "sourceAsset": {
          "address": "0x0...7ef",
          "symbol": "BAT",
          "decimals": "18"
        },
        "sourceAmount": "100000000000000000",
        "destinationAsset": {
          "address": "0x0...00",
          "symbol": "ETH",
          "decimals": "18"
        },
        "destinationAmount": "91588661679677",
        "orders": [
          {
            "sourceAsset": {
              "address": "0x0...ef",
              "symbol": "BAT",
              "decimals": "18"
            },
            "sourceAmount": "100000000000000000",
            "destinationAsset": {
              "address": "0x0...00",
              "symbol": "ETH",
              "decimals": "18"
            },
            "destinationAmount": "91588661679677",
            "exchange": {
              "id": 11,
              "name": "Uniswap"
            },
            "fee": {
              "percentage": "0.3",
              "amount": "300000000000000",
              "asset": {
                "address": "0x0...ef",
                "symbol": "BAT",
                "decimals": "18"
              }
            }
          }
        ],
        "runnerUpOrders": [
          {
            "sourceAsset": {
              "address": "0x0...ef",
              "symbol": "BAT",
              "decimals": "18"
            },
            "sourceAmount": "100000000000000000",
            "destinationAsset": {
              "address": "0x0...00",
              "symbol": "ETH",
              "decimals": "18"
            },
            "destinationAmount": "91176512702118",
            "exchange": {
              "id": 2,
              "name": "Kyber"
            },
            "fee": {
              "percentage": "0",
              "amount": "0",
              "asset": {
                "address": "0x0...7ef",
                "symbol": "BAT",
                "decimals": "18"
              }
            }
          }
        ]
      },
      {
        "sourceAsset": {
          "address": "0x0...00",
          "symbol": "ETH",
          "decimals": "18"
        },
        "sourceAmount": "91588661679677",
        "destinationAsset": {
          "address": "0x0...ef",
          "symbol": "BAT",
          "decimals": "18"
        },
        "destinationAmount": "100108060297981726",
        "orders": [
          {
            "sourceAsset": {
              "address": "0x0...00",
              "symbol": "ETH",
              "decimals": "18"
            },
            "sourceAmount": "91588661679677",
            "destinationAsset": {
              "address": "0x0...7ef",
              "symbol": "BAT",
              "decimals": "18"
            },
            "destinationAmount": "100108060297981727",
            "exchange": {
              "id": 2,
              "name": "Kyber"
            },
            "fee": {
              "percentage": "0",
              "amount": "0",
              "asset": {
                "address": "0x0...00",
                "symbol": "ETH",
                "decimals": "18"
              }
            }
          }
        ],
        "runnerUpOrders": [
          {
            "sourceAsset": {
              "address": "0x0...00",
              "symbol": "ETH",
              "decimals": "18"
            },
            "sourceAmount": "91588661679677",
            "destinationAsset": {
              "address": "0x0...7ef",
              "symbol": "BAT",
              "decimals": "18"
            },
            "destinationAmount": "99400877710875856",
            "exchange": {
              "id": 11,
              "name": "Uniswap"
            },
            "fee": {
              "percentage": "0.3",
              "amount": "274765985039",
              "asset": {
                "address": "0x0...00",
                "symbol": "ETH",
                "decimals": "18"
              }
            }
          }
        ]
      }
    ],
    "totleFee": {
      "asset": {
        "address": "0x0...00",
        "symbol": "ETH",
        "decimals": "18"
      },
      "percentage": "0.5",
      "amount": "457943308398"
    },
    "partnerFee": {
      "asset": {
        "address": "0x0...00",
        "symbol": "ETH",
        "decimals": "18"
      },
      "percentage": "0",
      "amount": "0"
    }
  }
]Param
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

