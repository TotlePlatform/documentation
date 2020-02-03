# Settings

To execute non-custodial swaps, the settlement Smart Contracts must have permission to move ERC20 tokens directly from counterparty wallets. The ERC20 standard specifies an [approve/transferFrom mechanism](https://theethereum.wiki/w/index.php/ERC20_Token_Standard#Approve_And_TransferFrom_Token_Balance) that DEX contracts use to accomplish this.

Trades that involve selling \(i.e., spending\) ERC20 tokens from the trader’s wallet will only execute successfully if the trader has first executed an `approve` transaction allowing the DEX settlement contract to transfer those tokens.

The number of coins that a trader allows the Smart Contract to spend is called an **allowance**. A trader making a single trade may set a fixed allowance, and those making several trades that spend the same token with the same contract may prefer to set an infinite allowance so that they don't have to replenish the allowance continually with additional `approve` transactions.

Every ERC20 token that a DEX contract will transfer from the trader’s wallet requires a prior `approve` transaction. When trading directly with multiple DEXs, an `approve` transaction needs to be executed for each token and each DEX. Totle simplifies this by only requiring users to approve an allowance for the Totle `TokenTransferProxy` Contract.

{% hint style="info" %}
#### Totle's TokenTransferProxy Contract Address

Totle's proxy contract address is **0x74758acfce059f503a7e6b0fc2c8737600f9f2c4**
{% endhint %}

Clients who wish to sell ERC20 tokens should execute the approve method of each ERC20 token contract by passing Totle’s `TokenTransferProxy` contract address. If the client sets the allowance for the exact amount of tokens to sell, then it must set the allowance again each time it wishes to sell more tokens. Alternatively, clients may set an unlimited allowance once, then trade the token an infinite number of times without having to go through this step again.

**Below is an example of how to set an unlimited allowance for the Totle** `TokenTransferProxy`

```javascript
const contract = new web3.eth.Contract(ERC20_ABI, TOKEN_ADDRESS)
const newAllowance = String((2 ** 256) - 1)
const data = contract.methods.approve(TOKEN_TRANSFER_PROXY_ADDRESS, newAllowance).encodeABI()
const txPromise = wallet.sendTransaction({
    to: TOKEN_ADDRESS,
    value: '0',
    gas,
    gasPrice,
    data
})
```

