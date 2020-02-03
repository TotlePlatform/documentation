---
description: Retrieve information about tokens supported by Totle.
---

# Tokens

{% api-method method="get" host="https://api.totle.com" path="/tokens" %}
{% api-method-summary %}
/tokens
{% endapi-method-summary %}

{% api-method-description %}
This endpoint returns a map of token names to contract addresses.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="tokens" type="string" required=false %}
The list of known ERC-20 tokens
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=false %}
The long name of the token
{% endapi-method-parameter %}

{% api-method-parameter name="symbol" type="string" required=false %}
The ticker symbol of the token
{% endapi-method-parameter %}

{% api-method-parameter name="address" type="string" required=false %}
The contract address that should be used to identify the token in API calls
{% endapi-method-parameter %}

{% api-method-parameter name="decimals" type="number" required=false %}
The number of decimal places implemented by the tokens
{% endapi-method-parameter %}

{% api-method-parameter name="tradeable" type="boolean" required=false %}
Whether the token can be traded on Totle
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Token information was successfully retrieved.
{% endapi-method-response-example-description %}

```python
{
  "tokens": [{
    "name": "Name of Coin",
    "symbol": "COINSYMBOL",
    "address": "0x...372",
    "decimals": 18,
    "tradable": true
  }]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% tabs %}
{% tab title="cURL" %}
```text
curl --request GET \
  --url https://api.totle.com/tokens
```
{% endtab %}

{% tab title="Node" %}
```javascript
var request = require("request");

var options = {method: 'GET', url: 'https://api.totle.com/tokens'};

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

url = URI("https://api.totle.com/tokens")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true
http.verify_mode = OpenSSL::SSL::VERIFY_NONE

request = Net::HTTP::Get.new(url)

response = http.request(request)
puts response.read_body
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
var data = null;

var xhr = new XMLHttpRequest();

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === this.DONE) {
    console.log(this.responseText);
  }
});

xhr.open("GET", "https://api.totle.com/tokens");

xhr.send(data);

```
{% endtab %}

{% tab title="Python" %}
```python
import requests

url = "https://api.totle.com/tokens"

response = requests.request("GET", url)

print(response.text)

```
{% endtab %}
{% endtabs %}


