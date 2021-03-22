### Place Batch Orders

> Place Batch Orders - Request Body

```json
{
    "orders": [
                {
                    "id"        : "sampleRequestId1",
                    "time"      : 1613878579169,
                    "symbol"    : "BTC-PERP",
                    "orderPrice": "34000",
                    "orderQty"  : "0.1",
                    "orderType" : "limit",
                    "side"      : "buy",
                    "respInst"  : "ACK"
                },
                {
                    "id"        : "sampleRequestId2",
                    "time"      : 1613878579169,
                    "symbol"    : "BTC-PERP",
                    "orderPrice": "35000",
                    "orderQty"  : "0.2",
                    "orderType" : "market",
                    "side"      : "buy",
                    "respInst"  : "ACK"
                }
              ]
}
```

> Place Batch Orders - Successful ACK Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": {
        "meta": {
            "action"  : "batch-place-order",
            "respInst": "ACK"
        },
        "orders": [
            {
                "id"       : "sampleRequestId1",
                "orderId"  : "a177c2a8cfe1U0123456789eqntvwWsy",
                "orderType": "Limit",
                "symbol"   : "BTC-PERP",
                "timestamp": 1613878579202
            },
            {
                "id"       : "sampleRequestId2",
                "orderId"  : "a177c2a8cfe1U0123456789equestId2",
                "orderType": "Market",
                "symbol"   : "BTC-PERP",
                "timestamp": 1613878579202
            }
        ]
    }
}
```
> Error Response

```json
{
    "ac": "FUTURES",
    "accountId": "sample-futures-account-id",
    "action": "batch-place-order",
    "code": 300013,
    "info": [
        {
            "code": 300013,
            "id": "sampleRequestId1",
            "message": "Some invalid order in this batch.",
            "reason": "INVALID_BATCH_ORDER",
            "symbol": "BTC-PERP"
        },
        {
            "code": 320008,
            "id": "sampleRequestId2",
            "message": "Futures account exposure higher than system acceptable level.",
            "reason": "FUTURES_TOO_RISKY",
            "symbol": "BTC-PERP"
        }
    ],
    "message": "Batch Order failed, please check each order info for detail.",
    "reason": "INVALID_BATCH_ORDER"
}
```

Place multiple orders in a batch. If any order(s) fails our basic check, the whole batch request will fail.

You may submit up to 10 orders at a time. Server will respond with error if you submit more than 10 orders.

**HTTP Request**

`POST /<grp>/api/pro/v2/futures/order/batch`

**Prehash String**

`<timestamp>+v2/futures/order/batch`

**Request Parameters**

 Name          | Data Type           | Description                
-------------- | ------------------- | -------------------------- 
 orders        | List                | List of order items                    
please refer to [placing new order](#new-order) for order item definition.

**respInst** field is required for market order and only *ACK* is allowed.
