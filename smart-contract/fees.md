# Fees

Fees are implemented as partner contracts. A partner contract is created by calling the function `registerPartner(address partnerBeneficiary, uint256 partnerPercentage)` on the PartnerRegistry \(currently on mainnet at `0xf3E5E76dabc9f4c479C258B4d7BB2F8250A8819C`\) where:

* **partnerBeneficiary** is the address you want to receive the fees at
* **partnerPercentage** is the percentage fee you want to take. `partnerPercentage` is out of 10^18 \(i.e., 10% is 10^17 and 0.1% is 10^15 \)

When `registerPartner` is called, the registry will emit a `PartnerRegistered(address partnerContract)` event \(where `partnerContract` is the address of the contract you've created\).

When you want to accrue fees, you will include `partnerContract` in your API request to the `/swap` or `/pay` endpoints:

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

The encoded payload that is returned will include your partner contract. When the transaction is executed, the fee \(in any ERC20\) will be sent to your partner contract. Note that the ethValue in the returned payload includes any fees defined by the partner contract for all buy orders. For sell orders, the fee will be deducted from the ETH returned to the user's wallet.

To collect your fees, someone must call the `payout()` function on your partner contract. Anybody can call this, and it will payout the appropriate fees to the `partnerBeneficiary` and to Totle.

The API has a default partner contract with a `partnerPercentage` of 0 and a `totlePercentage` of 0.25% \(which is used when one is not passed to the API\). The fee calculations would then be as follows:

* For direct token pairs where the sourceAsset is swapped for the destinationAsset \(and not through any base pairs\), the fee will be taken from the destinationAsset.
* For orders where the sourceAsset is swapped for a base asset, then the base asset is swapped for the destinationAsset, the fee will be calculated from the base asset.

If you include your partner contract in your request, the fees will be split evenly with Totle \(the minimum Totle will assess is 0.25%\).

**Do these fees not work for your business? Get in contact with us and we'll happily create a custom contract to meet your goals. Email:** [**partners@totle.com**](mailto:partners@totle.com)\*\*\*\*

