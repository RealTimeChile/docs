# Manual OAuth2 Authentication

**Manual OAuth2 Authentication**

In this **Chapter**, you will also find detailed example on how you can perform the above authentication steps **manually**, in case either your HTTP client or the HTTP library of your development language **does not** supports **OAuth2** authentication **natively**.

You should perform a **POST Request** to the **Access Token URL**, as seen in the above _authentication parameters_ table.

**HTTP POST Request**

`POST https://www.rti-sms.com/api/auth`

In this POST Request, you should send the following _Form URL-Encoded_ parameters in the **POST** body:

| Parameter | Description |
| :--- | :--- |
| **grant\_type** | Should be always set to **client\_credentials** |
| **client\_id** | [_Get it from web panel_](https://www.rti-sms.com) |
| **client\_secret** | [_Get it from web panel_](https://www.rti-sms.com) |

To **manually** authorize and fetch **access\_token**, use this code:

{% tabs %}
{% tab title="Bash" %}
```bash
curl -X "POST" "https://www.rti-sms.com/api/auth" \
     -H 'Content-Type: application/x-www-form-urlencoded; charset=utf-8' \
     --data-urlencode "grant_type=client_credentials" \
     --data-urlencode "client_id=YOUR_CLIENT_ID_HERE" \
     --data-urlencode "client_secret=YOUR_CLIENT_SECRET_HERE"
```
{% endtab %}

{% tab title="PHP" %}
```php
// get cURL resource
$ch = curl_init();

// set url
curl_setopt($ch, CURLOPT_URL, 'https://www.rti-sms.com/api/auth');

// set method
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, 'POST');

// return the transfer as a string
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);

// set headers
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  'Content-Type: application/x-www-form-urlencoded; charset=utf-8',
]);

// form body
$body = [
  'grant_type' => 'client_credentials',
  'client_id' => 'YOUR_CLIENT_ID_HERE',
  'client_secret' => 'YOUR_CLIENT_SECRET_HERE',
];
$body = http_build_query($body);

// set body
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS, $body);

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
    # You may modify this method according to your needs.
    # POST https://www.rti-sms.com/api/auth

    try:
        response = requests.post(
            url="https://www.rti-sms.com/api/auth",
            headers={
                "Content-Type": "application/x-www-form-urlencoded; charset=utf-8",
            },
            data={
                "grant_type": "client_credentials",
                "client_id": "YOUR_CLIENT_ID_HERE",
                "client_secret": "YOUR_CLIENT_SECRET_HERE",
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
// Node.JS
(function(callback) {
    'use strict';

    const httpTransport = require('https');
    const responseEncoding = 'utf8';
    const httpOptions = {
        hostname: 'www.rti-sms.com',
        port: '443',
        path: '/api/auth',
        method: 'POST',
        headers: {"Content-Type":"application/x-www-form-urlencoded; charset=utf-8"}
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
    request.write("grant_type=client_credentials&client_id=YOUR_CLIENT_ID_HERE&client_secret=YOUR_CLIENT_SECRET_HERE")
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
import org.apache.http.entity.ContentType;

public class SendRequest
{
  public static void main(String[] args) {
    sendRequest();
  }

  private static void sendRequest() {

    // Request (2) Duplicate (POST )

    try {

      // Create request
      Content content = Request.Post("https://www.rti-sms.com/api/auth")

      // Add headers
      .addHeader("Content-Type", "application/x-www-form-urlencoded; charset=utf-8")

      // Add body
      .bodyForm(Form.form()
      .add("grant_type", "client_credentials")
      .add("client_id", "YOUR_CLIENT_ID_HERE")
      .add("client_secret", "YOUR_CLIENT_SECRET_HERE")
      .build())

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

Make sure to replace `YOUR_CLIENT_ID_HERE` and `YOUR_CLIENT_SECRET_HERE` with your API client credentials.

If the **Authentication** is successful, API will respond with the HTTP Status `HTTP/1.1 200 OK` and in the response body you will get the **access\_token** and the **validity\_period** accordingly.

A successful authentication operation returns JSON structured like this:

```javascript
{
   "access_token":"eyXXXXXXSFSFZDSFSFSAFA.eyJpFSFSAGASXXVxzvzxWQHeSeIxMDAFSFAVZZIzNzM1MzYzODM3MzMifQ.p0kdoDSFSfzx2a$Ju8RCPAtLoLadSCZadasfaFa43",
   "validity_period":"3600"
}
```

As long as the **access\_token** is valid \(_current\_time_ **+** _validity\_period_\), you should use it in the _Authorization_ header parameter on every API call.

Example API Call, _Get more information about a specific sent SMS_:

```http
GET /api/sms/4421966385593 HTTP/1.1

Content-Type: application/json

Authorization: Bearer eyXXXXXXSFSFZDSFSFSAFA.eyJpFSFSAGASXXVxzvzxWQHeSeIxMDAFSFAVZZIzNzM1MzYzODM3MzMifQ.p0kdoDSFSfzx2a$Ju8RCPAtLoLadSCZadasfaFa43
```

{% hint style="danger" %}
All **not successful operations** are returned with a HTTP status different than`HTTP/1.1 200 OK`, such as `HTTP/1.1 401 Unauthorized` etc. For a **detailed list** of all possible returned errors, please see the [Errors Chapter](../errors/errors-codes.md).
{% endhint %}

