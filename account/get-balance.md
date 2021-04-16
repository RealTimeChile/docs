# Get Balance

Getting information about **how much money** are available in an **account**, is the only account related operation currently available in this API version. As long as your **access\_token** is **valid**, you can perform the following request:

#### HTTP GET Request <a id="http-get-request"></a>

```http
GET https://www.rti-sms.com/api/balance
```

#### HTTP GET Request's mandatory headers <a id="http-get-request-39-s-mandatory-headers"></a>

```http
Content-Type: application/json
Authorization: Bearer YOUR_ACCESS_TOKEN_HERE
```

{% tabs %}
{% tab title="Bash" %}
```bash
## Get Balance Operation
curl "https://www.rti-sms.com/api/balance" \
     -H 'Content-Type: application/json' \
     -H 'Authorization: Bearer ***** Hidden credentials *****'
```
{% endtab %}

{% tab title="PHP" %}
```php
// get cURL resource
$ch = curl_init();

// set url
curl_setopt($ch, CURLOPT_URL, 'https://www.rti-sms.com/api/balance');

// set method
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, 'GET');

// return the transfer as a string
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);

// set headers
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  'Content-Type: application/json',
  'Authorization: Bearer ***** Hidden credentials *****',
]);

// send the request and save response to $response
$response = curl_exec($ch);

// stop if fails
if (!$response) {
  die('Error: "' . curl_error($ch) . '" - Code: ' . curl_errno($ch));
}

echo 'HTTP Status Code: ' . curl_getinfo($ch, CURLINFO_HTTP_CODE) . PHP_EOL;
echo 'Response Body: ' . $response . PHP_EOL;

// close curl resource to free up system resources 
curl_close($ch);
```
{% endtab %}

{% tab title="Python" %}
```python
# Install the Python Requests library:
# `pip install requests`

import requests

def send_request():
    # Get Balance Operation
    # GET https://www.rti-sms.com/api/balance

    try:
        response = requests.get(
            url="https://www.rti-sms.com/api/balance",
            headers={
                "Content-Type": "application/json",
                "Authorization": "Bearer ***** Hidden credentials *****",
            },
        )
        print('Response HTTP Status Code: {status_code}'.format(
            status_code=response.status_code))
        print('Response HTTP Response Body: {content}'.format(
            content=response.content))
    except requests.exceptions.RequestException:
        print('HTTP Request failed')
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
// request Get Balance Operation 
(function(callback) {
    'use strict';

    const httpTransport = require('https');
    const responseEncoding = 'utf8';
    const httpOptions = {
        hostname: 'www.rti-sms.com',
        port: '443',
        path: '/api/balance',
        method: 'GET',
        headers: {"Content-Type":"application/json","Authorization":"Bearer ***** Hidden credentials *****"}
    };
    httpOptions.headers['User-Agent'] = 'node ' + process.version;

    // Paw Store Cookies option is not supported

    const request = httpTransport.request(httpOptions, (res) => {
        let responseBufs = [];
        let responseStr = '';

        res.on('data', (chunk) => {
            if (Buffer.isBuffer(chunk)) {
                responseBufs.push(chunk);
            }
            else {
                responseStr = responseStr + chunk;            
            }
        }).on('end', () => {
            responseStr = responseBufs.length > 0 ? 
                Buffer.concat(responseBufs).toString(responseEncoding) : responseStr;

            callback(null, res.statusCode, res.headers, responseStr);
        });

    })
    .setTimeout(0)
    .on('error', (error) => {
        callback(error);
    });
    request.write("")
    request.end();


})((error, statusCode, headers, body) => {
    console.log('ERROR:', error); 
    console.log('STATUS:', statusCode);
    console.log('HEADERS:', JSON.stringify(headers));
    console.log('BODY:', body);
});
```
{% endtab %}

{% tab title="Java" %}
```java
import java.io.IOException;
import org.apache.http.client.fluent.*;

public class SendRequest
{
  public static void main(String[] args) {
    sendRequest();
  }

  private static void sendRequest() {

    // Get Balance Operation (GET )

    try {

      // Create request
      Content content = Request.Get("https://www.rti-sms.com/api/balance")

      // Add headers
      .addHeader("Content-Type", "application/json")
      .addHeader("Authorization", "Bearer ***** Hidden credentials *****")

      // Fetch request and return content
      .execute().returnContent();

      // Print content
      System.out.println(content);
    }
    catch (IOException e) { System.out.println(e); }
  }
}
```
{% endtab %}
{% endtabs %}

If the **Get Balance** operation is successful, API will respond with the HTTP Status: `HTTP/1.1 200 OK` and in the response body you will get the **balance** variable with the amount of money available in the account as value.

A successful **get balance** operation returns JSON structured like this:

```bash
{"balance":"457.00"}
```

{% hint style="success" %}
Remember, if you don't supply an **access\_token** prefixed with the tag **`Bearer`** with a **single space** like in the examples above, or if you perform the API call with an expired **`access_token`**, API will respond with a **`HTTP 401 - Unauthorized`** with an empty body! In such cases and most probably if you are not using an **OAuth2** capable **HTTP Client** which may handle the authentication process for you, you should perform the **manual authentication** process again and use the new **`access_token`** for the subsequent API calls.
{% endhint %}



