### WS: Place Order 

> Request to place new order

```json
{
   "op"    : "req",
   "action": "place-order",
   "ac"    : "futures",         // the Account Category
   "id"    : "sampleRequestID", // the server will echo back this id in the ack message. 
   "args":{
      "time"      : 1613753879921,
      "symbol"    : "BTC-PERP",
      "orderPrice": "30000",
      "orderQty"  : "0.12",
      "orderType" : "limit",
      "side"      : "buy",
      "postOnly"  : false,
      "respInst"  : "ACK"
   }
}
```

> Successful ACK message

```json
{
   "m"     : "order",
   "code"  : 0,
   "id"    : "sampleRequestID",   // echo back the original request Id
   "action": "place-order",
   "ac"    : "FUTURES",
   "info": {
      "orderId": "s177bbb671b7U1234567890leOrderId",
      "symbol" : "BTC-PERP"
   }
}
```
> Error response message

```json
{
   "m"     : "order",
   "code"  : 300001,
   "id"    : "sampleRequestID",  // echo back the original request Id
   "action": "place-order",
   "ac"    : "FUTURES",
   "info": {
      "symbol"  : "BTC-PERP",
      "reason"  : "INVALID_PRICE",
      "errorMsg": "Order price is too low from market price."
   }
}
```

Place order via websocket 

**Request**

Make new order request follow the general websocket request rule, with proper place new order parameters as specified in rest api for *args* field.

see [placing order via RESTful API](#new-order).

*id*

As described in [Generate Order Id](#generate-order-id), the server uses a deterministic algorithm to compute the orderId based on client inputs. 
For every order request placed via WebSocket, **We strongly recommend you put a non-repeatable id**.

**Response**

Respond with *m* field as *order*, and *action* field as *place-order*; 
if you provide *id* in your request, it will be echoed back as *id* to help you identify; 
*code* field to indicate if this is a successful *zero* or failed *non-zero*.

*code=0* 

With *code* field as *zero* to indicate this new order request pass some basic sanity check, and has been sent to matching engine. 

*info* field provide some detail: if you provide *id* in your request, it will be echoed back as *id* to help you identify; we also provide server side generated *orderId*, which is the id you should use for future track or action on the order.  


*code=non-zero* 

With *code* field as *non-zero* to indicate there is some obvisous errors in your request. 

*info* field provide some detail: we also provide error *reason* and *errorMsg* detail.
