# Receive SMS \(MO\)

Our SMS API Platform will **POST** all the inbound MO SMS to user's specified **callback URL** in a similar way with _Delivery Reports_. As applied to _DLRs_, user's system/platform should returns a _HTTP Status Code_ **200**.

In order to setup your **Callback URL**, please _contact our customer support_.

Example JSON **POST** request for MO \(Inbound\) SMS Message:

```javascript
{
    "phone" : "447945223343",
    "originator" : "8300",
    "message" : "Test 1"
}
```

