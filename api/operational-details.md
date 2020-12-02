---
description: How the Totle API works.
---

# Operational Details

## Executing Trades

![](../.gitbook/assets/api-overview.jpg)

Finding and executing trades is a two-step process:

1. **Get orders to fill**: The client submits a request to the `/swap` endpoint that includes the tokens they want to buy and sell. Totle's Suggester calculates the best way to execute the buy and sell transactions using its aggregated order books and real-time price information. Suggester returns a response to the client that contains a signable transaction payload consisting of orders that can be settled on the blockchain.
2. **Submit signed orders**: The client digitally signs the transaction payload returned by Suggester and sends it to the Ethereum Network. The Totle Primary Contract translates the payload into a set of sub-transactions that execute on the involved exchanges. These exchanges execute transfers in the ERC-20 contracts for each trade.

## Signing and Submitting a Transaction

The response from the `swap` endpoint includes a payload that needs to be signed and submitted to the Ethereum network for mining. You can do this using the [web3](https://web3js.readthedocs.io/en/1.0/#) library's `signTransaction` and `sendTransaction` functions.

There are five steps you need to take to connect a wallet and get started with signing transactions from Totle.

#### 1. Get a Provider

Find a wallet provider that uses the [web3](https://web3js.readthedocs.io/en/1.0/#) library. Alternatively, with a supported browser, you can use the injected web3 provider. [Totle Swap](http://swap.totle.com/) uses [web3connect](https://github.com/web3connect/web3connect#individual-connectors), which allows for a choice of several web3 providers.

#### 2. Connect to a Wallet

Once you've added the wallet library to your application, you can connect to a wallet \(or an injected provider\).

```javascript
if (walletProvider) { // user defined provider
  this.web3 = new Web3(walletProvider)
} else if (window.ethereum) { // injected wallet provider (new standard)
  this.web3 = new Web3(window.ethereum)
  try {
    await window.ethereum.enable()
  } catch (error) {
    // User denied account access...
  }
} else if (window.web3) { // injected wallet provider (old standard)
  this.web3 = new Web3(window.web3.currentProvider)
}
```

#### 3. Fetch Transactions from the Totle API

Get Transactions from the Totle API using the following:

```javascript
const { success, response } = await fetch("https://api.totle.com/swap", requestObject)
```

#### 4. Parse the API Response

In the response from Totle's API is the transaction object you need. Look for it, and isolate the object for use in the next step. The object should look something like the following:

```javascript
"tx": {
    "to": "0x0d8775f648430679a709e98d2b0cb6250d2887ef",
    "from": "0x5c1739f2a9dcb46e5c2fbac81300af6369e167ef",
    "value": "0",
    "data": "0x...ff",
    "gasPrice": "15001500000",
    "gas": "47233",
    "nonce": "7"
}
```

#### 5. Send the Transaction

Once you have the transaction object, you can send it to the Ethereum network using the following code:

```javascript
for (const transaction of response.transactions) {
  // transaction.type // approval | swap
  web3.sendTransaction(transaction.tx)
    .on('transactionHash', (hash) => {
      console.log('transaction hash', hash)
    })
}
```

## Slippage

**Execution slippage** refers to the change between the quoted price and the actual execution price. You may specify what the allowable execution slippage is when you make a request to the API, otherwise, Totle will use a default value of 3%. Any trades where the execution slippage exceeds the allowable value will fail, and none of the client's tokens will move.

## Token Amounts

When providing token amounts to the API for the `/swap` endpoint, the amount you provide should be in the token's base unit of decimals.

The conversion factor to get this high-precision decimal number is `1*10^(x)` where `x` is the token decimals. For example, if you're working with 1 MKR, its representation using the token's base unit of decimals is 1000000000000000000 MKR.

## Gas

Most wallets provide you with the option of setting the gas price for the transaction before you sign and submit it for execution.

In general, setting a higher gas price results in the transaction getting mined sooner, since miners try to maximize the fees they collect when constructing blocks. However, setting a higher gas price is a common way to front-run DEX transactions, so some DEXs try to combat this by setting limits on the gas price. If you set a gas price above these limits, the transaction will fail.

The `/swap` endpoint includes gas price and limit in the transactions.

