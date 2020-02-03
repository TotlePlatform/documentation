---
description: Retrieve information about exchanges connected to Totle.
---

# Exchanges

{% api-method method="get" host="https://api.totle.com" path="/exchanges" %}
{% api-method-summary %}
/exchanges
{% endapi-method-summary %}

{% api-method-description %}
This endpoint returns a map of exchange names to exchange IDs.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="exchanges" type="object" required=false %}
The list of exchanges on which Totle trades
{% endapi-method-parameter %}

{% api-method-parameter name="id" type="number" required=false %}
The ID of the exchange 
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=false %}
The common name of the exchange
{% endapi-method-parameter %}

{% api-method-parameter name="enabled" type="boolean" required=false %}
Wether the `swap`endpoint is can return trades that will settle on that exchange
{% endapi-method-parameter %}

{% api-method-parameter name="iconURL" type="string" required=false %}
URL of the source for exchange's icon
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Exchange information successfully retrieved. 
{% endapi-method-response-example-description %}

```python
{
  "exchanges": [
    {
      "id": 2,
      "name": "Kyber",
      "enabled": true,
      "iconUrl": "https:\/\/s3.amazonaws.com\/totle-dex-icons\/Kyber.png"
    },
    {
      "id": 4,
      "name": "Bancor",
      "enabled": true,
      "iconUrl": "https:\/\/s3.amazonaws.com\/totle-dex-icons\/Bancor.png"
    },
    {
      //...
    }
  ],
  "success": true
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
  --url https://api.totle.com/exchanges
```
{% endtab %}

{% tab title="Node" %}
```javascript
var request = require("request");

var options = {method: 'GET', url: 'https://api.totle.com/exchanges'};

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

url = URI("https://api.totle.com/exchanges")

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

xhr.open("GET", "https://api.totle.com/exchanges");

xhr.send(data);
```
{% endtab %}

{% tab title="Python" %}
```python
import requests

url = "https://api.totle.com/exchanges"

response = requests.request("GET", url)

print(response.text)
```
{% endtab %}
{% endtabs %}

