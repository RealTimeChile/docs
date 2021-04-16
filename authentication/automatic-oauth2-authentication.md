# Automatic OAuth2 Authentication

#### Automatic OAuth2 Authentication <a id="automatic-oauth2-authentication"></a>

If your HTTP client supports **OAuth2** authentication **natively**, you only have to configure the _authentication parameters_ according to the above table.

By configuring the above parameters, you have just to perform the rest API calls \(View your Balance, Send SMS etc.\). Your **Oauth2** capable HTTP client will perform the **authentication** automatically for you **before** the first API request. If the **Authentication** is successful, SMS API will return an **Access Token** associated with a **Validity Period** in seconds. This **Access Token** for as long as is still **valid** \(according to **Validity Period**\), allows you to access all SMS API operations described in the current documentation without the need to perform subsequent authentications for each API call you perform.

Your **OAuth2** capable HTTP client will perform a new **Authentication** for you \(and it will fetch a new **Access Token** with an updated **Validity Period**\) just before the first API call that will be executed after the **Validity Period** of the **Access Token** expires.

