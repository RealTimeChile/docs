# Authentication Parameters

RealTime's SMS API implements **OAuth2** for it's authentication flow.

**OAuth doesn’t share password data** but instead uses **authorization tokens** to prove an identity between consumers and service providers. **OAuth2** is an authentication protocol that allows you to approve one application interacting with another on your behalf without giving away your password. All the **tokens** \(_Client ID, Client Secret and Access Token_\) are securely encrypted with [JWT](https://jwt.io/).

#### Authentication Parameters <a id="authentication-parameters"></a>

| Parameter | Description |
| :--- | :--- |
| Grant Type | Client Credentials |
| Client ID | [_Get it from web panel_](https://www.rti-sms.com) |
| Client Secret | [_Get it from web panel_](https://www.rti-sms.com) |
| Access Token URL | https://www.rti-sms.com/api/auth |

####  <a id="manual-oauth2-authentication"></a>



