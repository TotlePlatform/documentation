---
description: Execute a swap and a payment in a single transaction.
---

# Pay

{% api-method method="post" host="https://api.totle.com" path="/pay" %}
{% api-method-summary %}
/pay
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows payments to be made to a specified address.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="apiKey" type="string" required=false %}
The Totle partner ID
{% endapi-method-parameter %}

{% api-method-parameter name="partnerContract" type="string" required=false %}
The smart conntract address if you're a Totle partner
{% endapi-method-parameter %}

{% api-method-parameter name="address" type="string" required=false %}
The msg.sender wallet address. Although optional, you will only receive a payload if you include the address
{% endapi-method-parameter %}

{% api-method-parameter name="config" type="object" required=false %}
Transaction/trade-related configuration options
{% endapi-method-parameter %}

{% api-method-parameter name="config.exchanges" type="object" required=false %}
Information about the exchanges to be used \(or not used\)
{% endapi-method-parameter %}

{% api-method-parameter name="config.exchanges.list" type="array" required=false %}
IDs of the exchanges to whitelist/blacklist. Use /exchanges endpoint for IDs to use \(array of integers\)
{% endapi-method-parameter %}

{% api-method-parameter name="config.exchanges.type" type="string" required=false %}
Whether the exchange\(s\) should be whitelisted/blacklisted. Use `white` for whitelisting and `black` for blacklisting
{% endapi-method-parameter %}

{% api-method-parameter name="config.transactions" type="boolean" required=false %}
Whether transaction objects are returned or not. Setting this to `true` will require you to include `address`. If you just want to get the rate, set this to false
{% endapi-method-parameter %}

{% api-method-parameter name="config.fillNonce" type="boolean" required=false %}
Whether the `nonce` field in the transaction objects are populated or not. Defaults to `true`
{% endapi-method-parameter %}

{% api-method-parameter name="config.skipBalanceChecks" type="boolean" required=false %}
Whether the API should validate the source asset balance of the wallet given in the address field. Defaults to `true`
{% endapi-method-parameter %}

{% api-method-parameter name="swap" type="object" required=true %}
Information about the single swap to be executed \(**submit either `swap` OR `swaps` ; do not submit both to the API**\)
{% endapi-method-parameter %}

{% api-method-parameter name="swap.sourceAsset" type="string" required=true %}
Identifier of the token to sell \(either token address OR symbol\)
{% endapi-method-parameter %}

{% api-method-parameter name="swap.destinationAsset" type="string" required=true %}
Identifier of the token to buy \(either token address OR symbol\)
{% endapi-method-parameter %}

{% api-method-parameter name="swap.sourceAmount" type="integer" required=true %}
The amount of tokens to sell
{% endapi-method-parameter %}

{% api-method-parameter name="swap.destinationAmount" type="integer" required=true %}
The amount of tokens to purchase
{% endapi-method-parameter %}

{% api-method-parameter name="swap.maxSource" type="integer" required=false %}
The maximum amount of token to be sold when all costs are factored in
{% endapi-method-parameter %}

{% api-method-parameter name="swap.destinationAddress" type="string" required=true %}
The wallet to which the `destinationAsset` should be paid to
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
If the payment was successful.
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

{% tabs %}
{% tab title="cURL" %}
```text
curl -X POST \
  https://api.totle.com/pay \
  -H 'content-type: Application/JSON' \
  -d '{"swap":{"sourceAsset":"ETH","destinationAsset":"DAI","destinationAmount":"1000000000000000000", "destinationAddress": "0x583d03451406d179182efc742a1d811a9e34c36b"}}'
```
{% endtab %}

{% tab title="Node" %}
```javascript
var request = require("request")

var body = {
    "swap": {
        "sourceAsset": "ETH",
        "destinationAsset": "DAI",
        "destinationAmount": "1000000000000000000",
        "destinationAddress": "0x583d03451406d179182efc742a1d811a9e34c36b"
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

url = URI("https://api.totle.com/pay")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Post.new(url)
request["content-type"] = 'Application/JSON'
request.body = "{\"swap\":{\"sourceAsset\":\"ETH\",\"destinationAsset\":\"DAI\",\"destinationAmount\":\"1000000000000000000\", \"destinationAddress\": \"0x583d03451406d179182efc742a1d811a9e34c36b\"}}"

response = http.request(request)
puts response.read_body
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
var data = "{\"swap\":{\"sourceAsset\":\"ETH\",\"destinationAsset\":\"DAI\",\"destinationAmount\":\"1000000000000000000\", \"destinationAddress\": \"0x583d03451406d179182efc742a1d811a9e34c36b\"}}";

var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === 4) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "https://api.totle.com/pay");
xhr.setRequestHeader("content-type", "Application/JSON");

xhr.send(data);
```
{% endtab %}

{% tab title="Python" %}
```python
import requests

url = "https://api.totle.com/pay"

payload = "{\"swap\":{\"sourceAsset\":\"ETH\",\"destinationAsset\":\"DAI\",\"destinationAmount\":\"1000000000000000000\", \"destinationAddress\": \"0x583d03451406d179182efc742a1d811a9e34c36b\"}}"
headers = {
    'content-type': "Application/JSON"
}

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```
{% endtab %}
{% endtabs %}

