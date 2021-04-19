# Receive Delivery Reports \(DLR\)

Delivery statuses also known as **Delivery Reports**, are **automatically forwarded** to the user system/platform. When an **SMS delivery report** is received by our **SMS API Platform**, the **DLR information** is immediately forwarded to your **specified DLR Callback URL** via a **POST** request in _JSON_ format \(_see the related example_\).

In order to setup your **Callback URL**, please _contact our customer support_.

#### Important <a id="important"></a>

Our SMS API Platform assumes that user's system/platform _successfully accepted_ the callback request, **only** if returns a _HTTP Status Code_ **200**. The HTTP Status Code **200** is considered as a valid acknowledgement of DLR information from the user side. In case user's system/platform either **not returns the above status code** _or_ is **not accessible at all**, our platform will **re-attempt** the **POST** request containing the DLR information, based on the following schedule:

| Attempt \# | Time |
| :--- | :--- |
| 1st Attempt | **instantly** |
| 2nd Attempt | after **5** minutes |
| 3rd Attempt | after **15** minutes |
| 4th Attempt | after **30** minutes |
| 5th Attempt | after **1** hour |
| 6th Attempt | after **5** hours |
| 7th Attempt | after **24** hours |

After _7th Attempt_ and if the user's system still fails to acknowledge DLR information, there will be **no more attempts** to transmit and information will be discarded.

#### Delivery Status Codes <a id="delivery-status-codes"></a>

The JSON field **status** may have one of the following values:

| Status Code Value | Description |
| :--- | :--- |
| 0 | NO STATUS |
| 1 | DELIVERED |
| 2 | FAILED / Erroneous Number |
| 3 | FAILED / Network Error |
| 4 | PENDING |
| 5 | EXPIRED |

DLR information POSTed to the **callback** URL, have the following parameters:

```javascript
{
    "id" : "543521789981",
    "phone" : "447945223343",
    "status" : 1,
    "date" : "2020-11-11 11:11:11"
}
```

