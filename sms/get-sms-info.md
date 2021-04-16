# Get SMS Info

Operation **Get SMS Info** is useful in order to get information about a **single submission**. In order to perform this operation, you need to supply a **submission ID**.

#### HTTP GET Request <a id="http-get-request-2"></a>

```http
GET https://www.rti-sms.com/api/sms/4193366853543393
```

#### HTTP GET Request's mandatory headers <a id="http-get-request-39-s-mandatory-headers-2"></a>

```http
Content-Type: application/json
Authorization: Bearer YOUR_ACCESS_TOKEN_HERE
```

{% hint style="info" %}
You must replace `4193366853543393` with a **submission ID** from a past **Send SMS** operation.
{% endhint %}

{% tabs %}
{% tab title="Bash" %}
```bash
curl "https://www.rti-sms.com/api/sms/4193366853543393" \
     -H 'Content-Type: application/json' \
     -H 'Authorization: Bearer ***** Hidden credentials *****'
```
{% endtab %}

{% tab title="PHP" %}
```php
// get cURL resource
$ch = curl_init();

// set url
curl_setopt($ch, CURLOPT_URL, 'https://www.rti-sms.com/api/sms/4193366853543393');

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
    try:
        response = requests.get(
            url="https://www.rti-sms.com/api/sms/4193366853543393",
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
// request Request Duplicate 
(function(callback) {
    'use strict';

    const httpTransport = require('https');
    const responseEncoding = 'utf8';
    const httpOptions = {
        hostname: 'www.rti-sms.com',
        port: '443',
        path: '/api/sms/4193366853543393',
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


    try {

      // Create request
      Content content = Request.Get("https://www.rti-sms.com/api/sms/4193366853543393")

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

If the **Get SMS Info** operation is successful, API will respond with the HTTP Status: `HTTP/1.1 200 OK` and in the response body you will get a **JSON Object** containing details about a **single** SMS submission.

A successful **get sms info** operation returns JSON structured like this:

```javascript
{
   "id":"4193366853543393",
   "timestamps":{
      "registered":1600351683,
      "sent":1600351694,
      "done":1600355610
   },
   "info":{
      "status":{
         "code":"1",
         "status":"DELIVERED"
      },
      "cost":1,
      "operator":{
         "id":"188",
         "name":"Entel Pcs",
         "mcc":"730",
         "mnc":"10"
      }
   }
}
```

Please see the table bellow for the available fields in this object:

#### SMS Info Object Fields <a id="sms-info-object-fields"></a>

Field \| Type \| Description id \| **String** \| The **unique Id** of this submission. In this response, this field does not provide new information since you have requested the information of this submission using exactly the same Id. It is included in the response for convenience. timestamps \| **Object** \| This JSON Object contains the UNIX/EPOCH **timestamps** of the three stages of the sms submission. More information are included in a separate table below. info \| **Object** \| Contains 2 child objects, the object **status** providing indication of the delivery status of this SMS, as well as the object **operator** providing **accurate information** of the network operator to which this SMS was sent.

#### Field **timestamps** structure <a id="field-timestamps-structure"></a>

Field \| Type \| Description registered \| **Integer** \| Timestamp in which a **single SMS submission** was registered \(but **not yet** send by\) to **RealTime's** system. This value could not be **zero**. sent \| **Integer** \| Timestamp in which a **single SMS submission** was sent to **recipient's** network operator. done \| **Integer** \| Timestamp in which we got a **final** outcome from a **single SMS submission**. Either if the SMS is **DELIVERED**, or **REJECTED** by the network, or **EXPIRED** etc, all such events specify a **final** event.

#### Field **info**/**status** structure <a id="field-info-status-structure"></a>

| Field | Type | Description |
| :--- | :--- | :--- |
| status | "String" | Specifies the **delivery status** of a **single SMS submission**. |
| code | "String" | The numerical representation of **status** field. |

The above **status** field could take one of the **following** values:

* PENDING
* SENT
* DELIVERED
* REJECTED
* UNDELIVERED
* EXPIRED
* UNKNOWN

#### Field **info**/**operator** structure <a id="field-info-operator-structure"></a>

| Field | Type | Description |
| :--- | :--- | :--- |
| id | **String** | The **unique ID** of a **network operator**, according to **RealTime's** database. |
| name | **String** | The **name** of a **network operator**. |
| mcc | **String** | Numeric value. Specifies the **country** of a **network operator**. Full name is: **Mobile Country Code**. |
| mnc | **String** | Numeric value. Specifies a **network operator** within **the same mcc value**. |

{% hint style="info" %}
For **more information** please see the **code samples** included in the current documentation.
{% endhint %}

