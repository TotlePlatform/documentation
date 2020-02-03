---
description: >-
  If the Totle API is unable to handle your request, it will respond with the
  appropriate response code and error message.
---

# Error Messages

| Error | Error Code | Error Message | Additional Information |
| :--- | :--- | :--- | :--- |
| RequestValidationError | 1000 | Request parameters are invalid. | You can get familiar with Totle’s API using our [API explorer](https://explorer.totle.com/). |
| StructuralError | 1100 | Request object is incorrectly structured. |  |
| MissingRequiredParameterError | 1101 | Request parameter PARAMETER NAME is missing. |  |
| IncorrectFormatError | 1102 | Request input in incorrect format. | Based on scenario, the error may be due to: the request exchange list isn't formatted correctly; the request includes both `swap` and `swaps` objects; `swaps` isn't formatted as an array; the request includes both source _and_ destination amounts; the request sets `strictDestination` with `sourceAmount` |
| UnknownParameterError | 1103 | Request parameter NAME is not recognized | You can get familiar with Totle’s API using our [API explorer](https://explorer.totle.com/). |
| InputValueError | 1200 | Request input value is invalid. |  |
| AmountError | 1201 | Swap amounts must be greater than 0. |  |
| InvalidAddressError | 1202 | The wallet address ADDRESS format is invalid. |  |
| TokenNotFoundError | 1203 | This token ADDRESS is not found. |  |
| InvalidSlippagePercentError | 1204 | The maximum MARKET/EXECUTION slippage must be between 0-99. | Make sure your request is formatted properly with values that fall in the specified range. |
| InvalidFillPercentError | 1205 | Minimum fill percent must be between 1-100. | Use minimum fill to specify the quantity of tokens you need guaranteed during transaction execution. |
| IsOptionalError | 1206 | Is optional must be boolean \(true or false\). | This boolean controls whether or not the order can be skipped. This could be helpful when you have an array of orders that you would like to submit through Totle, and you don’t want the entire set of swaps to fail from one failed swap.  |
| PartnerError | 1300 | An error occurred validating partner. | To learn more about deploying partner contracts and how to earn and claim fees, please see our [fees section](../smart-contract/fees.md). |
| PartnerContractAddressNotRegisteredError | 1301 | This partner contract address ADDRESS is not registered. | To learn more about deploying partner contracts and how to earn and claim fees, please see our [fees section](../smart-contract/fees.md). |
| ExecutionError | 2000 | An internal error occurred while finding suggestions. |  |
| NotEnoughVolumeError | 2100 | We couldn’t find enough orders to fill your request for SOURCE SYMBOL =&gt; DESTINATION SYMBOL. Please try again later. |  |
| MarketSlippageTooHighError | 2101 | The market slippage is higher than the acceptable percentage. | The market slippage you specified was not met. This means the best price we could find for you at your order quantity is out of the tolerable acceptance when compared to an order quantity of 0.1 units of the sourceAsset. To learn more about slippage, visit our [slippage section](operational-details.md#slippage). |
| NoUsableExchangeError | 2102 | No exchange from the list EXCHANGES is usable. |  |
| TokenNotTradableError | 2103 | TOKEN NAME - TOKEN ADDRESS is not tradable. |  |
| SourceAmountGreaterThanMaxError | 2104 | Required source amount for swap is greater than the requested max. |  |
| WalletError | 3000 | Error with user’s wallet. |  |
| CompoundLiquidityError | 3101 | You have outstanding positions on Compound and cannot sell below your liquidation position. | Visit [Compound](https://compound.finance/) for more information.  |

