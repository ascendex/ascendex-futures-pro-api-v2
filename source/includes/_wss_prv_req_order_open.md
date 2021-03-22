### WS: Query Open Orders

> Requesting open orders on symbol BTC-PERP

```json
{
   "op"    : "req",
   "id"    : "abc123456",
   "action": "futures-open-orders",
   "args":{
      "symbol":"BTC-PERP"
   }
}
```

> Open orders response

```json
{
   "m":"futures-open-orders",
   "code":0,
   "id":"abc123456",
   "ac":"FUTURES",
   "data":[
      {
         "ac":"FUTURES",
         "accountId":"sample-futures-account-id",
         "time":1615696544843,
         "orderId":"r1782f04c58aU3792951278sbtcp7EbA",
         "seqNum":13,
         "orderType":"Limit",
         "execInst":"NULL_VAL",
         "side":"Sell",
         "symbol":"BTC-PERP",
         "price":"66000",
         "orderQty":"0.0001",
         "stopPrice":"0",
         "stopBy":"market",
         "status":"New",
         "lastExecTime":1615696544851,
         "lastQty":"0",
         "lastPx":"0",
         "avgFilledPx":"0",
         "cumFilledQty":"0",
         "fee":"0",
         "cumFee":"0",
         "feeAsset":"USDT",
         "errorCode":"",
         "posStopLossPrice":"0",
         "posStopLossTrigger":"None",
         "posTakeProfitPrice":"0",
         "posTakeProfitTrigger":"None"
      },
      ...
   ]
}
```

> Error response message

```json
{
   "m":"error",
   "id":"abc123456",
   "code":100005,
   "reason":"INVALID_WS_REQUEST_DATA",
   "info":"Missing required parameter: args"
}
```

You can request the open order via websocket by a `futures-open-orders` action. 

The request schema:

 Name          | Data Type           | Description                
-------------- | ------------------- | -------------------------- 
 op            | String              | `req`                      
 action        | String              | `futures-open-orders`  
 id            | String              | for result match purpose       
 args:symbol  | Optional[String]    | add the (optional) symbol filter, see below for details.

The `symbol` key in the `args` map allows you to customize the symbol filter in a flexible way:

* to query open orders of the **a specific symbol**, set `symbol` to a valid symbol code. For instance, `{"symbol": "BTC-PERP"}`
* to query **all open orders**, you may simply omit the `symbol` key (`{}`). 

   
