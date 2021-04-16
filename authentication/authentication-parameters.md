# Authentication

RealTime's SMS API implements **OAuth2** for it's authentication flow.

**OAuth doesn’t share password data** but instead uses **authorization tokens** to prove an identity between consumers and service providers. **OAuth2** is an authentication protocol that allows you to approve one application interacting with another on your behalf without giving away your password. All the **tokens** \(_Client ID, Client Secret and Access Token_\) are securely encrypted with [JWT](https://jwt.io/).

#### Authentication Parameters <a id="authentication-parameters"></a>

| Parameter | Description |
| :--- | :--- |
| Grant Type | Client Credentials |
| Client ID | [_Get it from web panel_](https://www.rti-sms.com) |
| Client Secret | [_Get it from web panel_](https://www.rti-sms.com) |
| Access Token URL | https://www.rti-sms.com/api/auth |

#### Automatic OAuth2 Authentication <a id="automatic-oauth2-authentication"></a>

If your HTTP client supports **OAuth2** authentication **natively**, you only have to configure the _authentication parameters_ according to the above table.

By configuring the above parameters, you have just to perform the rest API calls \(View your Balance, Send SMS etc.\). Your **Oauth2** capable HTTP client will perform the **authentication** automatically for you **before** the first API request. If the **Authentication** is successful, SMS API will return an **Access Token** associated with a **Validity Period** in seconds. This **Access Token** for as long as is still **valid** \(according to **Validity Period**\), allows you to access all SMS API operations described in the current documentation without the need to perform subsequent authentications for each API call you perform.

Your **OAuth2** capable HTTP client will perform a new **Authentication** for you \(and it will fetch a new **Access Token** with an updated **Validity Period**\) just before the first API call that will be executed after the **Validity Period** of the **Access Token** expires.

#### Manual OAuth2 Authentication <a id="manual-oauth2-authentication"></a>

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

If the **Authentication** is successful, API will respond with the HTTP Status: `HTTP/1.1 200 OK` and in the response body you will get the **access\_token** and the **validity\_period** accordingly.

As long as the **access\_token** is valid \(_current tume_ **+** _validity\_period_\), you should use it in the _Authorization_ header parameter on every API call.

Example API Call, _Get more information about a specific sent SMS_:

`GET /api/sms/4421966385593 HTTP/1.1`

`Content-Type: application/json`

`Authorization: Bearer eyXXXXXXSFSFZDSFSFSAFA.eyJpFSFSAGASXXVxzvzxWQHeSeIxMDAFSFAVZZIzNzM1MzYzODM3MzMifQ.p0kdoDSFSfzx2a$Ju8RCPAtLoLadSCZadasfaFa43`

{% api-method method="get" host="https://www.rti-sms.com" path="/api/sms/4421966385593" %}
{% api-method-summary %}
Example API Call, get more information about specific sent SMS
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Content-Type" type="string" required=true %}
application/json
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-form-data-parameters %}
{% api-method-parameter name="Authorization" type="string" required=true %}
`Bearer eyXXXXXXSFSFZDSFSFSAFA.eyJpFSFSAGASXXVxzvzxWQHeSeIxMDAFSFAVZZIzNzM1MzYzODM3MzMifQ.p0kdoDSFSfzx2a$Ju8RCPAtLoLadSCZadasfaFa43`
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

