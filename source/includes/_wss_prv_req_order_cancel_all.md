### WS: Cancel All Orders

> Request to cancel all existing open orders 

```json
{
   "op"    : "req",
   "action": "cancel-all",
   "ac"    : "futures",
   "id"    : "sampleRequestId", // server will echo back this Id.
   "args": {   // you can also omit the args field
   }
}
```

> Request to cancel existing open order related to symbol "BTC-PERP"

```json
{
   "op"    : "req",
   "action": "cancel-all",
   "ac"    : "futures",
   "id"    : "sampleRequestId", // server will echo back this Id.
   "args":{ 
        "symbol": "BTC-PERP"     
   }
}
```

> Successful ACK message

```json
{
   "m"     : "order",
   "code"  : 0,
   "action": "cancel-all",
   "ac"    : "FUTURES",
   "id"    : "sampleRequestId", // echo back the original request Id
   "info":{
      "symbol":""
   }
}
```

> Error response message

```json
{
   "m"     : "order",
   "code"  : 300012,
   "action": "cancel-all",
   "ac"    : "FUTURES",
   "id"    : "sampleRequestId", // echo back the original request Id
   "info":{
      "symbol"  : "",
      "reason"  : "INVALID_PRODUCT",
      "errorMsg": "Invalid Product Symbol"
   }
}
```

Cancel all open orders on account level via websocket with optional symbol.

**Request**

Make general websocket request with `action` field as `cancel-All` and set proper `ac` value(`futures`), and provide *symbol* value in *args*.

**Response**

With *code* field as *zero* to indicate this cancel all order request has been received by server and sent to matching engine. 

*info* field provide some detail: if you provide *symbol* in your request to cancel orders.

With *code* field as *non-zero* to indicate there is some obvisous errors in your request. 

*info* field provide some detail: we also provide error *reason* and *errorMsg* detail.
