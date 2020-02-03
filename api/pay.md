---
description: Execute a swap and a payment in a single transaction.
---

# Pay

{% api-method method="post" host="https://api.totle.com" path="/pay" %}
{% api-method-summary %}
/pay
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows allows payments to be made to the specified party.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="apiKey" type="string" required=true %}
The Totle partner ID
{% endapi-method-parameter %}

{% api-method-parameter name="partnerContract" type="string" required=false %}
The Smart Contract address if you're a Totle partner
{% endapi-method-parameter %}

{% api-method-parameter name="address" type="string" required=true %}
Your wallet address
{% endapi-method-parameter %}

{% api-method-parameter name="config" type="object" required=false %}
Transaction/trade-related information
{% endapi-method-parameter %}

{% api-method-parameter name="config.exchanges" type="object" required=false %}
Information about the exchanges to be used \(or not used\)
{% endapi-method-parameter %}

{% api-method-parameter name="config.exchanges.list" type="array" required=false %}
IDs of the exchanges to whitelist/blacklist. Use /exchanges endpoint for IDs used \(array of integers\)
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
Information about the token being traded for another token \(if necessary\) and then transferred to the wallet specified
{% endapi-method-parameter %}

{% api-method-parameter name="swap.sourceAsset" type="string" required=true %}
The token to be sold
{% endapi-method-parameter %}

{% api-method-parameter name="swap.destinationAsset" type="string" required=true %}
The token to be bought
{% endapi-method-parameter %}

{% api-method-parameter name="swap.destinationAmount" type="integer" required=true %}
The amount of token to be bought \(corresponds to the token amount to be sold\)
{% endapi-method-parameter %}

{% api-method-parameter name="swap.maxSource" type="integer" required=false %}
The maximum amount of token to be sold when all costs are factored in
{% endapi-method-parameter %}

{% api-method-parameter name="swap.destinationAddress" type="string" required=true %}
The wallet to which the token should be deposited
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

{% tabs %}
{% tab title="cURL" %}
```text
curl --request POST \
  --url https://api.totle.com/pay \
  --header 'content-type: application/json' \
  --data '{"config":{"exchanges":{"type":""},"transactions":"true","fillNonce":"true","skipBalanceChecks":"false"},"swap":{"sourceAsset":"","destinationAsset":"","destinationAmount":"","maxSource":"","destinationAddress":""}}'
```
{% endtab %}

{% tab title="Node" %}
```javascript
var request = require("request");

var options = {
  method: 'POST',
  url: 'https://api.totle.com/pay',
  headers: {'content-type': 'application/json'},
  body: '{"config":{"exchanges":{"type":""},"transactions":"true","fillNonce":"true","skipBalanceChecks":"false"},"swap":{"sourceAsset":"","destinationAsset":"","destinationAmount":"","maxSource":"","destinationAddress":""}}'
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

url = URI("https://api.totle.com/pay")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true
http.verify_mode = OpenSSL::SSL::VERIFY_NONE

request = Net::HTTP::Post.new(url)
request["content-type"] = 'application/json'
request.body = "{\"config\":{\"exchanges\":{\"type\":\"\"},\"transactions\":\"true\",\"fillNonce\":\"true\",\"skipBalanceChecks\":\"false\"},\"swap\":{\"sourceAsset\":\"\",\"destinationAsset\":\"\",\"destinationAmount\":\"\",\"maxSource\":\"\",\"destinationAddress\":\"\"}}"

response = http.request(request)
puts response.read_body
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
var data = "{\"config\":{\"exchanges\":{\"type\":\"\"},\"transactions\":\"true\",\"fillNonce\":\"true\",\"skipBalanceChecks\":\"false\"},\"swap\":{\"sourceAsset\":\"\",\"destinationAsset\":\"\",\"destinationAmount\":\"\",\"maxSource\":\"\",\"destinationAddress\":\"\"}}";

var xhr = new XMLHttpRequest();

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === this.DONE) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "https://api.totle.com/pay");
xhr.setRequestHeader("content-type", "application/json");

xhr.send(data);
```
{% endtab %}

{% tab title="Python" %}
```python
import requests

url = "https://api.totle.com/pay"

payload = "{\"config\":{\"exchanges\":{\"type\":\"\"},\"transactions\":\"true\",\"fillNonce\":\"true\",\"skipBalanceChecks\":\"false\"},\"swap\":{\"sourceAsset\":\"\",\"destinationAsset\":\"\",\"destinationAmount\":\"\",\"maxSource\":\"\",\"destinationAddress\":\"\"}}"
headers = {'content-type': 'application/json'}

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```
{% endtab %}
{% endtabs %}

