### WS: Cancel Order

> Request to cancel existing open order

```json
{
   "op"    : "req",
   "action": "cancel-order",
   "ac"    : "futures",
   "id"    : "sampleRequestId",    // server will echo back this Id.
   "args":{
      "time":1613744943323,
      "orderId":"s177bab1b474U5051470287bbtcpKiOR",
      "symbol":"BTC-PERP"
   }
}
```

> Successful ACK message

```json
{
   "m"     : "order",
   "action": "cancel-order",
   "ac"    : "FUTURES",
   "id"    : "sampleRequestId", // echo back the original request Id
   "code":0,
   "info":{
      "orderId": "s177bab1b474U5051470287bbtcpKiOR",
      "symbol" : "BTC-PERP"
   }
}
```

> Error response message

```json
{
   "m"     : "order",
   "action": "cancel-order",
   "ac"    : "FUTURES",
   "code"  : 300006,
   "id"    : "sampleRequestId", // echo back the original request Id
   "info":{
      "symbol"  : "BTC-PERP",
      "reason"  : "INVALID_ORDER_ID",
      "errorMsg": "Client Order Id too Long: s177bab1b474U5051470287bbtcpKiOR1"
   }
}
```

Cancel an existing open order via websocket 

**Request**

Make order cancelling request follow the general websocket request rule by setting `action` to be `cancel-orde`, with proper cancel order parameters as specified in rest api for *args* field.

**Response**

Respond with *m* field as *order*, and *action* field as *cancel-order*; 
*code* field to indicate if this is a successful *zero* or failed *non-zero*.

*code=0* 

With *code* field as *zero* to indicate this cancel order request pass some basic sanity check, and has been sent to matching engine. 

*info* field provide some detail: if you provide *symbol* in your request, it will be echoed back as *symbol* to help you idintify; we also echo back target *orderId* to be cancelled.  

*code=non-zero*

With *code* field as *non-zero* to indicate there is some obvisous errors in your cancel order request. 

*info* field provide some detail: we also provide error *reason* and *errorMsg* detail.
