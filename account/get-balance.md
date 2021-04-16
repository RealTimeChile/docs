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

If the **Get Balance** operation is successful, API will respond with the HTTP Status: `HTTP/1.1 200 OK` and in the response body you will get the **balance** variable with the amount of money available in the account as value.

