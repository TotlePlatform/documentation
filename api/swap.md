---
description: Swap tokens at the best pricing available.
---

# Swap

{% api-method method="post" host="https://api.totle.com" path="/swap" %}
{% api-method-summary %}
/swap
{% endapi-method-summary %}

{% api-method-description %}
The endpoint allows you to trade one token for the equivalent value of another token. This can be used to trade single pairs or multiple pairs.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="apiKey" type="string" required=true %}
Your Totle partner identifier
{% endapi-method-parameter %}

{% api-method-parameter name="partnerContract" type="string" required=false %}
The smart contract address if you're a Totle partner
{% endapi-method-parameter %}

{% api-method-parameter name="address" type="string" required=false %}
The `msg.sender` wallet address. Although optional, you will only receive a payload if you include the address
{% endapi-method-parameter %}

{% api-method-parameter name="config" type="object" required=false %}
Transaction/trade-related configuration options
{% endapi-method-parameter %}

{% api-method-parameter name="config.exchanges" type="object" required=false %}
Information about the exchanges to be used \(or not used\)
{% endapi-method-parameter %}

{% api-method-parameter name="config.exchanges.list" type="array" required=false %}
IDs of the exchanges to whitelist/blacklist. Use /exchanges endpoint for IDs to use \(an array of integers\)
{% endapi-method-parameter %}

{% api-method-parameter name="config.exchanges.type" type="string" required=false %}
Whether the exchange\(s\) should be whitelisted/blacklisted. Use `white` for whitelisting and `black` for blacklisting
{% endapi-method-parameter %}

{% api-method-parameter name="config.transactions" type="boolean" required=false %}
Whether transactions objects are returned or not. The default setting for this parameter is `false` which will return a quote. Settings this to `true` will execute a transaction and requires you to include the address. We encourage you to only set this to `true` when you intend to submit a trade.
{% endapi-method-parameter %}

{% api-method-parameter name="config.fillNonce" type="boolean" required=false %}
Whether the `nonce` field in the transaction objects are populated or not. Defaults to `true`
{% endapi-method-parameter %}

{% api-method-parameter name="config.skipBalanceChecks" type="boolean" required=false %}
Whether the API should validate the source asset balance of the wallet given in the address field. Defaults to `true`
{% endapi-method-parameter %}

{% api-method-parameter name="swap" type="object" required=true %}
Information about the single trading pair to be executed \(**submit either `swap` OR `swaps`; do not submit both to the API**\)
{% endapi-method-parameter %}

{% api-method-parameter name="swap.sourceAsset" type="string" required=true %}
Identifier of the token to sell \(either token address OR symbol\)
{% endapi-method-parameter %}

{% api-method-parameter name="swap.sourceAmount" type="integer" required=true %}
The amount of tokens to sell in the token's base unit of decimals \(**include either `sourceAmount` OR `destinationAmount`**\)
{% endapi-method-parameter %}

{% api-method-parameter name="swap.destinationAsset" type="string" required=false %}
Identifier of the token to buy \(either token address or symbol\)
{% endapi-method-parameter %}

{% api-method-parameter name="swap.isOptional" type="boolean" required=false %}
If this is `true` then the entire transaction won't revert if this swap fails. Defaults to `false`
{% endapi-method-parameter %}

{% api-method-parameter name="swap.maxExecutionSlippagePercent" type="integer" required=false %}
Percentage of maximum acceptable slippage of quoted rate from the API response to the settled rate on-chain. Defaults to 3. Value must be between 0-99, inclusive
{% endapi-method-parameter %}

{% api-method-parameter name="swaps" type="array" required=true %}
Your Totle information about the swap \(one or more\) to be executed \(**submit either `swap` OR `swaps`; do not submit both to the API**\)
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
If the swap was successful.
{% endapi-method-response-example-description %}

```text
{
    "success": true,
    "response": {
        "id": "0x...353",
        "summary": [ ... ],
        "transactions": [ ... ],
        "expiration": { ... }
    }
}

For failures:

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
To execute multiple swaps, submit a request using the `swaps` array of objects, where each object within the array contains information about a single swap \(i.e., to swap two token pairs, include two objects within the `swaps` array\).
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
```text
curl -X POST \
  https://api.totle.com/swap \
  -H 'content-type: Application/JSON' \
  -d '{ 
   "swap":{ 
      "sourceAsset":"ETH",
      "destinationAsset":"DAI",
      "sourceAmount":"1000000000000000000",
      "maxMarketSlippagePercent":"10",
      "maxExecutionSlippagePercent":"3"
   }
}'
```
{% endtab %}

{% tab title="Node" %}
```javascript
var request = require("request")

var body = { 
   "swap":{ 
      "sourceAsset":"ETH",
      "destinationAsset":"DAI",
      "sourceAmount":"1000000000000000000",
      "maxMarketSlippagePercent":"10",
      "maxExecutionSlippagePercent":"3"
   }
}

var options = {
  method: 'POST',
  url: 'https://api.totle.com/swap',
  headers: {'content-type': 'application/json'},
  body: JSON.stringify(body)
}

request(options, function (error, response, body) {
  if (error) throw new Error(error)

  console.log(body)
})
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
require 'uri'
require 'net/http'

url = URI("https://api.totle.com/swap")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Post.new(url)
request["content-type"] = 'Application/JSON'
request.body = "{\"swap\":{\"sourceAsset\":\"ETH\",\"destinationAsset\":\"DAI\",\"sourceAmount\":\"1000000000000000000\",\"maxMarketSlippagePercent\":\"10\",\"maxExecutionSlippagePercent\":\"3\"}}"

response = http.request(request)
puts response.read_body
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
var data = "{\"swap\":{\"sourceAsset\":\"ETH\",\"destinationAsset\":\"DAI\",\"sourceAmount\":\"1000000000000000000\",\"maxMarketSlippagePercent\":\"10\",\"maxExecutionSlippagePercent\":\"3\"}}";

var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === 4) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "https://api.totle.com/swap");

xhr.send(data);
```
{% endtab %}

{% tab title="Python" %}
```python
import requests

url = "https://api.totle.com/swap"

payload = "{\"swap\":{\"sourceAsset\":\"ETH\",\"destinationAsset\":\"DAI\",\"sourceAmount\":\"1000000000000000000\",\"maxMarketSlippagePercent\":\"10\",\"maxExecutionSlippagePercent\":\"3\"}}"
headers = {
    'content-type': "Application/JSON"
    }

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```
{% endtab %}
{% endtabs %}

