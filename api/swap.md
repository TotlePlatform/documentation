---
description: Swap tokens at the best pricing available.
---

# Swap

{% api-method method="post" host="https://api.totle.com" path="/tokens" %}
{% api-method-summary %}
/swap
{% endapi-method-summary %}

{% api-method-description %}
The endpoint allows you to trade one token for the equivalent value of another token. This can be used to trade single pairs or multiple pairs.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="apiKey" type="string" required=false %}
Your Totle partner identifier
{% endapi-method-parameter %}

{% api-method-parameter name="partnerContract" type="string" required=false %}
The Smart Contract address if you're a Totle partner
{% endapi-method-parameter %}

{% api-method-parameter name="address" type="string" required=false %}
Your wallet address
{% endapi-method-parameter %}

{% api-method-parameter name="config" type="object" required=false %}
Transaction/trade-related information
{% endapi-method-parameter %}

{% api-method-parameter name="config.exchanges" type="object" required=false %}
Information about the exchanges to be used \(or not used\)
{% endapi-method-parameter %}

{% api-method-parameter name="config.exchanges.list" type="array" required=false %}
IDs of the exchanges to whitelist/blacklist. Use /exchanges endpoint for IDs used \(an array of integers\)
{% endapi-method-parameter %}

{% api-method-parameter name="config.exchanges.type" type="string" required=false %}
Whether the exchange should be whitelisted/blacklisted. Use `white` for whitelisting and `black` for blacklisting
{% endapi-method-parameter %}

{% api-method-parameter name="config.transactions" type="boolean" required=false %}
Whether a response is returned or not \(allows the submission of a request for accurate pricing information even if there's no intention to execute any trades\)
{% endapi-method-parameter %}

{% api-method-parameter name="config.fillNonce" type="boolean" required=false %}
Whether the `nonce` field in the response is populated or not \(allows for manual population of `nonce` in cases where there are multiple transactions present\)
{% endapi-method-parameter %}

{% api-method-parameter name="config.skipBalanceChecks" type="boolean" required=false %}
Whether the API should validate the source asset balance of the wallet given in the address field
{% endapi-method-parameter %}

{% api-method-parameter name="swap" type="object" required=true %}
Information about the single trading pair to be executed \(**submit either swap or swaps; do not submit both to the API**\)
{% endapi-method-parameter %}

{% api-method-parameter name="swap.sourceAsset" type="string" required=true %}
Identifier of the token to sell \(either token address or symbol\)
{% endapi-method-parameter %}

{% api-method-parameter name="swap.sourceAmount" type="integer" required=true %}
The amount of tokens to sell in the token's base unit of decimals \(include either sourceAmount or destinationAmount\)
{% endapi-method-parameter %}

{% api-method-parameter name="swap.destinationAmount" type="integer" required=true %}
The amount of tokens to buy in the token's base unit of decimals \(include either sourceAmount or destinationAmount\) 
{% endapi-method-parameter %}

{% api-method-parameter name="swap.isOptional" type="boolean" required=false %}
Whether this trading pair can be skipped or not \(default is false\)
{% endapi-method-parameter %}

{% api-method-parameter name="swap.minFillPercent" type="integer" required=false %}
Percentage of minimum acceptable destination amount to receive. Value must be between 1-100, inclusive
{% endapi-method-parameter %}

{% api-method-parameter name="swap.maxMarketSlippagePercent" type="integer" required=false %}
Percentage of maximum acceptable market price slippage that can occur based off of 0.1 unit of source token while finding best rates off-chain. Value must be between 1-99, inclusive
{% endapi-method-parameter %}

{% api-method-parameter name="swap.maxExecutionSlippagePercent" type="integer" required=false %}
Percentage of maximum acceptable slippage of market rate from the time the API finds the rate and executing swap on-chain. Value must be between 1-99, inclusive
{% endapi-method-parameter %}

{% api-method-parameter name="swaps" type="array" required=true %}
Your Totle Information about the trading pairs \(two or more\) to be executed \(**submit either swap or swaps; do not submit both to the API**\) identifier
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
If the swap was successful.
{% endapi-method-response-example-description %}

```
{
    "success": true,
    "response": {
        "id": "0x...353",
        "summary": [ ... ],
        "transactions": [ ... ],
        "expiration": { ... }
    }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
If there was an issue with the call. 
{% endapi-method-response-example-description %}

```
{
    "success": false,
    "response": {
        "code": 3100,
        "name": "Error Name",
        "message": "Error message",
        "link": "",
        "info": "Detailed error information"
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
**Swap Vs Swaps - Executing Multiple Swaps in One Call**  
To rebalance a portfolio using multiple token pair trades, submit a request using the `swaps` array of objects, where each object within the array contains information about a single trading pair \(i.e., to swap two token pairs, include two objects within the `swaps` array\).
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
```text
curl --request POST \
  --url https://api.totle.com/swap \
  --header 'content-type: application/json' \
  --data '{"config":{"exchanges":{"type":""},"transactions":"true","fillNonce":"true","skipBalanceChecks":"false"},"swap":{"sourceAsset":"","destinationAsset":"","sourceAmount":"","destinationAmount":"","isOptional":"false","minFillPercent":"","maxMarketSlippagePercent":"10","maxExecutionSlippagePercent":"3"}}'
```
{% endtab %}

{% tab title="Node" %}
```javascript
var request = require("request");

var options = {
  method: 'POST',
  url: 'https://api.totle.com/swap',
  headers: {'content-type': 'application/json'},
  body: '{"config":{"exchanges":{"type":""},"transactions":"true","fillNonce":"true","skipBalanceChecks":"false"},"swap":{"sourceAsset":"","destinationAsset":"","sourceAmount":"","destinationAmount":"","isOptional":"false","minFillPercent":"","maxMarketSlippagePercent":"10","maxExecutionSlippagePercent":"3"}}'
};

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
require 'uri'
require 'net/http'
require 'openssl'

url = URI("https://api.totle.com/swap")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true
http.verify_mode = OpenSSL::SSL::VERIFY_NONE

request = Net::HTTP::Post.new(url)
request["content-type"] = 'application/json'
request.body = "{\"config\":{\"exchanges\":{\"type\":\"\"},\"transactions\":\"true\",\"fillNonce\":\"true\",\"skipBalanceChecks\":\"false\"},\"swap\":{\"sourceAsset\":\"\",\"destinationAsset\":\"\",\"sourceAmount\":\"\",\"destinationAmount\":\"\",\"isOptional\":\"false\",\"minFillPercent\":\"\",\"maxMarketSlippagePercent\":\"10\",\"maxExecutionSlippagePercent\":\"3\"}}"

response = http.request(request)
puts response.read_body

```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
var data = "{\"config\":{\"exchanges\":{\"type\":\"\"},\"transactions\":\"true\",\"fillNonce\":\"true\",\"skipBalanceChecks\":\"false\"},\"swap\":{\"sourceAsset\":\"\",\"destinationAsset\":\"\",\"sourceAmount\":\"\",\"destinationAmount\":\"\",\"isOptional\":\"false\",\"minFillPercent\":\"\",\"maxMarketSlippagePercent\":\"10\",\"maxExecutionSlippagePercent\":\"3\"}}";

var xhr = new XMLHttpRequest();

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === this.DONE) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "https://api.totle.com/swap");
xhr.setRequestHeader("content-type", "application/json");

xhr.send(data);
```
{% endtab %}

{% tab title="Python" %}
```python
import requests

url = "https://api.totle.com/swap"

payload = "{\"config\":{\"exchanges\":{\"type\":\"\"},\"transactions\":\"true\",\"fillNonce\":\"true\",\"skipBalanceChecks\":\"false\"},\"swap\":{\"sourceAsset\":\"\",\"destinationAsset\":\"\",\"sourceAmount\":\"\",\"destinationAmount\":\"\",\"isOptional\":\"false\",\"minFillPercent\":\"\",\"maxMarketSlippagePercent\":\"10\",\"maxExecutionSlippagePercent\":\"3\"}}"
headers = {'content-type': 'application/json'}

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)

```
{% endtab %}
{% endtabs %}

