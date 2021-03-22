### Cancel Batch Orders

> Cancel Batch Orders - Request Body

```json
{
   "orders":[
      {
         "id":"sampleRequestId1",
         "orderId":"a177c2a8cfe1U0123456789eqntvwWsy",
         "symbol":"BTC-PERP",
         "time":1613900544076
      },
      {
         "id":"sampleRequestId2",
         "orderId":"a177c2a8cfe1U0123456789equestId2",
         "symbol":"BTC-PERP",
         "time":1613900544076
      }
   ]
}
```

> Cancel Batch Orders - Successful ACK Response (Status 200, code 0)

```json
{
   "code":0,
   "data":{
      "meta":{
         "action":"batch-cancel-order",
         "respInst":"ACK"
      },
      "orders":[
         {
            "id":"sampleRequestId1",
            "orderId":"a177c2a8cfe1U0123456789eqntvwWsy",
            "orderType":"",
            "symbol":"BTC-PERP",
            "timestamp":1613900544091
         },
         {
            "id":"sampleRequestId2",
            "orderId":"a177c2a8cfe1U0123456789equestId2",
            "orderType":"",
            "symbol":"BTC-PERP",
            "timestamp":1613900544168
         }
      ]
   }
}
```


Cancel multiple orders in a batch. If any order(s) fails our basic check, the whole batch request will fail.

You may submit up to 10 orders to cancel at a time. Server will respond with error if you submit more than 10 orders.

**HTTP Request**

`DELETE /<grp>/api/pro/v2/futures/order/batch`

**Prehash String**

`<timestamp>+v2/futures/order/batch`

**Request Parameters**

 Name          | Data Type           | Description                
-------------- | ------------------- | -------------------------- 
 orders        | List                | List of order items to cancel                   
please refer to [cancel order](#cancel-order) for order item definition


