### New Order 

> Successful Response

```json
{
    "code": 0,
    "data": {
        "meta": {
            "action"  : "place-order",
            "id"      : "abcd1234abcd1234",
            "respInst": "ACCEPT"   // ACK, ACCEPT, or DONE
        },
        "order": {
            "ac"          : "FUTURES",
            "accountId"   : "sample-futures-account-id",
            "seqNum"      : 14,    // sequence number, also -1 in ACK mode
            "time"        : 1605677683714,
            "orderId"     : "sample-order-id",
            "orderType"   : "Limit",
            "side"        : "Buy",
            "symbol"      : "BTC-PERP",
            "price"       : "9500",
            "orderQty"    : "0.1",
            "stopPrice"   : "0",
            "stopBy"      : "market",
            "status"      : "New",
            "lastExecTime": 1605677684479,
            "lastPx"      : "0",
            "lastQty"     : "0",
            "avgFilledPx" : "0",
            "cumFilledQty": "0",
            "fee"         : "0",
            "cumFee"      : "0",
            "feeAsset"    : "USDT",
            "errorCode"   : ""
        }
    }
}
```

> Error Response

```json
{
    "ac": "FUTURES",
    "accountId": "sample-futures-account-id",
    "action": "place-order",
    "code": 300014,
    "info": {
        "id": "abcd1234abcd1234",
        "symbol": "BTC-PERP"
    },
    "message": "Order price doesn't conform to the required tick size: 1",
    "reason": "TICK_SIZE_VIOLATION"
}
```

**HTTP Request**

`POST /<grp>/api/pro/v2/futures/order`

**Prehash String**

`<timestamp>+v2/futures/order`

**Request Parameters**

PARAMETER                                   | TYPE      | REQUIRED | DESCRIPTION
------------------------------------------- |---------- | -------- | ---------------
id                                          | String    |          | >=9 chars (letter and digit number only). Optional but recommended. We echo it back to help you match response with request. By setting this field, you can obtain the orderId before sending the request. It is also useful when you place order in batch mode.
time                                        | Long      | Yes      | Milliseconds since UNIX epoch in UTC. We do not process request placed more than 30 seconds ago.
symbol                                      | String    | Yes      | e.g. `BTC-PERP`
price                                       | String    |          | Required for `Limit` and `StopLimit` orders
orderQty                                    | String    | Yes      | Order size. Please set scale properly for each symbol.
[orderType](#order-type-ordertype)          | ENUM      | Yes      | 
[side](#side-side)                          | ENUM      | Yes      |
[respInst](#response-type-respinst)         | ENUM      |          | `ACK` for limit order and `Done` for market order by default
postOnly                                    | Boolean   |          | `false` by default
stopPrice                                   | String    |          | required for `StopLimit` and `StopMarket` orders
[timeInForce](#time-in-force-timeinforce)   | ENUM      |          | `GTC` by default
[execInst](#execution-instruction-execinst) | ENUM      |          | 
posStopLossPrice                            | String    |          | position stop loss price
posTakeProfitPrice                          | String    |          | position take profit price


