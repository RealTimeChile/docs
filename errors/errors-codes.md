# Errors Codes

{% hint style="info" %}
This API is implemented as a `Restful API`, which means that the `application errors` are returned with the proper **`non 200 OK`** HTTP Response.
{% endhint %}

The RealTime SMS v.2 API uses the following error codes:

#### Error Codes <a id="error-codes"></a>

| Error Code | Meaning |
| :---: | :--- |
| 400 | `Bad Request` -- Your request is invalid. SMS API returns this error in cases of **malformed** data in your request, such as incorrect **client credentials** or **access token** format, e.t.c. Such errors **never** specify errors such as incorrect **client credentials** \(but in correct format\). |
| 401 | `Unauthorized` -- Either your **client credentials** are not **valid** or your **access\_token** is expired and you should perform the **authentication**, **again**. |
| 403 | `Forbidden` -- You have tried to access a **not allowed** operation for your account. |
| 404 | `Not Found` -- If your **URL** is correct, then you will get this error in **Get Sms Info** operation, when the **submission id** you supplied is **incorrect**. As a result, the specified SMS message could not be found. |
| 405 | `Method Not Allowed` -- If you attempt to perform an API call operation using the wrong method. For example, if an operation needs a _POST_ request and you perform a _PUT_ request, you should see this error. |
| 406 | `Not Acceptable` -- Currently, SMS API returns this type of error when the **SMS Sender** you have entered in your **Send SMS** operation, either is in wrong format, or is **not allowed** for use in your account. |
| 429 | `Too Many Requests` -- Possibly a threshold limit is applied to your account. |
| 500 | `Internal Server Error` -- We had a problem with our server. Try again later. |
| 503 | `Service Unavailable` -- Mostly like error no. 500, this error usually specifies a **temporary error** in our systems. At most cases, you don't need to take any action since everything should work as expected, moments later. |

