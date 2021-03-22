### Cancel Order 

> Response

```json
{
    "code": 0,
    "data": {
        "meta": {
            "action"  : "cancel-order",       // action
            "id"      : "abcd1234abcd1234",   // user provided ID
            "respInst": "ACCEPT"              // response instruction
        },
        "order": {
            "ac"          : "FUTURES",                    // account category
            "accountId"   : "sample-futures-account-id",  // account ID
            "seqNum"      : 14,                           // sequence number
            "time"        : 1605677683714,                // order creation time (UTC time in milliseconds)
            "orderId"     : "sample-order-id",            // order ID
            "orderType"   : "Limit",                      // order type
            "side"        : "Buy",                        // side
            "symbol"      : "BTC-PERP",                   // contract symbol
            "price"       : "9500",                       // order price 
            "orderQty"    : "0.1",                        // order qty
            "stopPrice"   : "0",                          // stop price
            "stopBy"      : "market",                     // stop price trigger 
            "status"      : "Canceled",                   // order status
            "lastExecTime": 1605677684479,                // last execution time (UTC time in milliseconds)
            "lastPx"      : "0",                          // last filled price
            "lastQty"     : "0",                          // last filled quantity
            "avgFilledPx" : "0",                          // average filled price of all fills 
            "cumFilledQty": "0",                          // cummulative filled quantity
            "fee"         : "0",                          // fee of the last fill
            "cumFee"      : "0",                          // cummulative fee
            "feeAsset"    : "USDT",                       // fee asset
            "errorCode"   : ""                            // error code
        }
    }
}
```

**HTTP Request**

`DELETE /<grp>/api/pro/v2/futures/order`

**Prehash String**

`<timestamp>+v2/futures/order`

**Request Parameters**

PARAMETER                           | TYPE   | REQUIRED | DESCRIPTION
----------------------------------- |--------| -------- | ------------------------------------------------------ 
id                                  | String |          | >=9 chars (letter and digit number only). Optional but recommended. We echo it back to help you match response with request. This is especially useful when you cancel in batch mode.
orderId                             | String |   Yes    | 32 chars order id. You should set the value to be the orderId of the target order you want to cancel.
symbol                              | String |   Yes    | Symbol of the order to cancel
time                                | Long   |   Yes    | milliseconds since UNIX epoch in UTC. We do not process request sent more than 30 seconds ago.
[respInst](#response-type-respinst) | ENUM   |          | `ACK` by default

**Response**



*respInst*

