### List Open Orders

> Response

```json
{
    "code": 0,
    "data": [
        {
            "ac"          : "FUTURES",                   // account category
            "accountId"   : "sample-futures-account-id", // account ID
            "seqNum"      : 14,                          // sequence number
            "time"        : 1605677683714,               // order creation time
            "orderId"     : "sample-order-id",           // order ID
            "orderType"   : "Limit",                     // order type
            "side"        : "Buy",                       // order side
            "symbol"      : "BTC-PERP",                  // contract symbol
            "price"       : "9500",                      // order price
            "orderQty"    : "0.1",                       // order quantity
            "stopPrice"   : "0",                         // stop price
            "stopBy"      : "market",                    // stop price trigger         
            "status"      : "New",                       // order status 
            "lastExecTime": 1605677684479,               // last execution time
            "lastPx"      : "0",                         // last filled price 
            "lastQty"     : "0",                         // last filled quantity
            "avgFilledPx" : "0",                         // average filled price of all fills
            "cumFilledQty": "0",                         // cummulative filled quantity
            "fee"         : "0",                         // fee of the last fill
            "cumFee"      : "0",                         // cummulative fee 
            "feeAsset"    : "USDT",                      // fee asset
            "errorCode"   : ""                           // error code
        }
    ]
}
```

**HTTP Request**

`POST /<grp>/api/pro/v2/futures/order/open`

**Prehash String**

`<timestamp>+v2/futures/order/open`


