# Send SMS

SMS operations available in **RealTime's V.2 SMS API**. Our Programmable SMS API helps you to add robust messaging capabilities to your applications. Using the SMS v.2 API, you can **send** SMS messages and **track their delivery status**.

### Send SMS <a id="send-sms"></a>

**Send SMS** operation is the operation you should use for send SMS messages.

#### HTTP POST Request <a id="http-post-request-2"></a>

```bash
POST https://www.rti-sms.com/api/sms
```

#### HTTP POST Request's mandatory headers <a id="http-post-request-39-s-mandatory-headers"></a>

```http
Content-Type: application/json
Authorization: Bearer YOUR_ACCESS_TOKEN_HERE
```

In the **POST** request's **body**, you should send a **JSON** object with the following parameters:

#### Parameters in POST BODY's JSON Object <a id="parameters-in-post-body-39-s-json-object"></a>

| Parameter | Type | Description |
| :--- | :--- | :--- |
| recipients | **Array** | Array of one or more **mobile numbers** |
| sender | **String** | Sender/Originator of the SMS message. |
| message | **Object** | Contains the SMS message variables. Please see **the separate table below**. |

#### Parameters in _message_ JSON Object <a id="parameters-in-message-json-object"></a>

**As referenced in the above table**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| charset | **Number** | This parameter specifies the **character encoding** of the SMS. In this chapter you can find a list of the supported charset values. |
| text | **String** | The text of the SMS message. |

{% tabs %}
{% tab title="Bash" %}
```bash
## Example using curl
curl -X "POST" "https://www.rti-sms.com/api/sms" \
     -H 'Content-Type: application/json' \
     -H 'Authorization: Bearer ***** Hidden credentials *****' \
     -d $'{
  "recipients": [
    "+56900000000"
  ],
  "message": {
    "charset": 0,
    "text": "libizon adikestr 85f0f569cb 1287c690e0"
  },
  "sender": "96000"
}'
```
{% endtab %}

{% tab title="PHP" %}
```php
// get cURL resource
$ch = curl_init();

// set url
curl_setopt($ch, CURLOPT_URL, 'https://www.rti-sms.com/api/sms');

// set method
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, 'POST');

// return the transfer as a string
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);

// set headers
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  'Content-Type: application/json',
  'Authorization: Bearer ***** Hidden credentials *****',
]);

// json body
$json_array = [
  'recipients' => [
    '+56900000000'
  ],
  'message' => [
    'charset' => 0,
    'text' => 'libizon adikestr 85f0f569cb 1287c690e0'
  ],
  'sender' => '96000'
]; 
$body = json_encode($json_array);

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
import json


def send_request():
    # Request
    # POST https://www.rti-sms.com/api/sms

    try:
        response = requests.post(
            url="https://www.rti-sms.com/api/sms",
            headers={
                "Content-Type": "application/json",
                "Authorization": "Bearer ***** Hidden credentials *****",
            },
            data=json.dumps({
                "recipients": [
                    "+56900000000"
                ],
                "message": {
                    "charset": 0,
                    "text": "libizon adikestr 85f0f569cb 1287c690e0"
                },
                "sender": "96000"
            })
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
// Node.JS Example
(function(callback) {
    'use strict';

    const httpTransport = require('https');
    const responseEncoding = 'utf8';
    const httpOptions = {
        hostname: 'www.rti-sms.com',
        port: '443',
        path: '/api/sms',
        method: 'POST',
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
    request.write("{\"recipients\":[\"+56900000000\"],\"sender\":\"96000\",\"message\":{\"charset\":0,\"text\":\"libizon adikestr 85f0f569cb 1287c690e0\"}}")
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

    // Request (POST )

    try {

      // Create request
      Content content = Request.Post("https://www.rti-sms.com/api/sms")

      // Add headers
      .addHeader("Content-Type", "application/json")
      .addHeader("Authorization", "Bearer ***** Hidden credentials *****")

      // Add body
      .bodyString("{\"recipients\": [\"+56900000000\"],\"message\": {\"charset\": 0,\"text\": \"libizon adikestr 85f0f569cb 1287c690e0\"},\"sender\": \"96000\"}", ContentType.APPLICATION_JSON)

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

A successful **send sms** operation returns JSON structured like this:

```javascript
{
   "submissions":[
      {
         "status":"submitted",
         "submissionId":"4193366853543393"
      }
   ]
}
```

{% hint style="warning" %}
Parameter`charset` of SMS message should be used **with care** since **affects the proper display** of the sms message in recipient's mobile phone. If a message uses characters not included in the _GSM 7-bit default alphabet_ \(empty charset value or charset=0\), you may consider to use the **Unicode Character Set**, otherwise all the non supported characters **may not** be displayed as expected.
{% endhint %}

If the **Send SMS** operation is successful, API will respond with the HTTP Status: `HTTP/1.1 200 OK` and in the response body you will get the **submissions** variable containing _information_ of each **sms submission** you made in the current operation.

Please note that in the **Send SMS** operation, **each recipient number** produces a **separate submission**. For example, if in the _Send SMS_ operation you include **2** recipient numbers, expect to see **2** results contained in the **submissions** variable, returned by the API.

In the **table** below, please see the fields of each **submission** result:

| Field | Type | Description |
| :--- | :--- | :--- |
| status | **String** | Specifies the **result** of a **single submission**. Possible values are contained in a _separate table_, below. |
| submissionId | **String** | The **unique ID** of a **single submission**. **Note: This field exists only if status field equals to "submitted"!** |

#### Possible **status** values <a id="possible-status-values"></a>

| Value | Description |
| :--- | :--- |
| submitted | Specifies a **successful** SMS Submission |
| account\_no\_balance | Specifies a **not successful** SMS Submission, because the **balance** of your account is **exhausted**. |
| unknown\_error | Specifies a **not successful** SMS Submission, because of an **internal error**. Usually such errors are **temporary**, but if the issue **persists**, please contact the customer support. |

#### Field **operator** structure <a id="field-operator-structure"></a>

| Field | Type | Description |
| :--- | :--- | :--- |
| id | **String** | The **unique ID** of a **network operator**, according to **RealTime's** database. |
| name | **String** | The **name** of a **network operator**. |
| mcc | **String** | Numeric value. Specifies the **country** of a **network operator**. Full name is: **Mobile Country Code**. |
| mnc | **String** | Numeric value. Specifies a **network operator** within **the same mcc value**. |

{% hint style="success" %}
Remember - if you don't supply an **`access_token`** prefixed with the tag **`Bearer`** with a **single space** like in the examples above, or if you perform the API call with an expired **`access_token`**, API will respond with a **`HTTP 401 - Unauthorized`** with an empty body! In such cases and most probably if you are not using an **OAuth2** capable **HTTP Client** which may handle the authentication process for you, you should perform the **manual authentication** process again and use the new **`access_token`** for the subsequent API calls.
{% endhint %}

#### Supported Charset Values <a id="supported-charset-values"></a>

| Value | Description |
| :--- | :--- |
| 0 | Request from SMS API to choose the **default character** set value for the current SMS text |
| 1 | GSM 7-bit ASCII |
| 6 | All characters in **Hexadecimal Unicode UCS2 format**. e.g. for **āĉġ** SMS text should be **010101090121** |
| 8 | **Latin Characters URL Encoded** \(à, è, ì, ò, ù\). e.g. for **àü** SMS text should be **%7F%7E** |

