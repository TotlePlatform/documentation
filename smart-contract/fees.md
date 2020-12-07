# Fees

Fees are implemented as partner contracts. A partner contract is created by calling the function `registerPartner(address partnerBeneficiary, uint256 partnerPercentage)` on the PartnerRegistry \(currently on mainnet at `0x02e2795f544f61af8897199335f4d8d149be4a38`\) where:

* **partnerBeneficiary** is the address you want to receive the fees at
* **partnerPercentage** is the percentage fee you want to take. `partnerPercentage` is out of 10^18 \(i.e., 10% is 10^17 and 0.1% is 10^15 \)

When `registerPartner` is called, the registry will emit a `PartnerRegistered(address partnerContract)` event \(where `partnerContract` is the address of the contract you've created\).

When you want to accrue fees, you will include `partnerContract` in your API request to the `/swap`endpoint:

```javascript
{
    "apiKey": "",
    "partnerContract": "",
    "address": "0x5...7eF",
    "config": {
        "exchanges": {
            "list": [],
            "type": ""
        },
        "transactions": bool,
        "fillNonce": bool,
        "skipBalanceChecks": bool
    },
    "swap": {
        "sourceAsset": "",
        "destinationAsset": "",
        "sourceAmount": int, // send either sourceAmount OR destinationAmount, not both
        "minFillPercent": int,
        "maxMarketSlippagePercent": int,
        "maxExecutionSlippagePercent": int,
        "destinationAmount": int,
        "isOptional": bool
    }
}
```

The encoded payload that is returned will include your partner contract. When the transaction is executed, the fee \(in any ERC20/ETH\) will be sent to your partner contract.

To collect your fees, someone must call the `payout()` function on your partner contract. Anybody can call this, and it will payout the appropriate fees to the `partnerBeneficiary` and to Totle.

The API has a default partner contract with a `partnerPercentage` of 0 and a `totlePercentage` of 0 \(which is used when one is not passed to the API\). When a fee is selected, a default 50:50 profit split will be applied. If you expect large trading volumes then we're happy to discuss a custom fee structure.  

**Email:** [**partners@totle.com**](mailto:partners@totle.com)\*\*\*\*

