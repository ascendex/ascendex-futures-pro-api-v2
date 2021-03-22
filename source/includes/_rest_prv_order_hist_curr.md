### List Current History Orders

> Current History Orders - Request Body

```json
{
   "symbol":"BTC-PERP",
   "n":20,
   "executedOnly":true
}
```

> Successful Response (Status 200, code 0)

```json
{
   "code":0,
   "data":[
      {
         "ac":"FUTURES",
         "accountId":"sampleFuturesAccountId",
         "avgFilledPx":"58501",
         "cumFee":"0.058501",
         "cumFilledQty":"0.001",
         "errorCode":"",
         "execInst":"NULL_VAL",
         "fee":"0.058501",
         "feeAsset":"USDT",
         "lastExecTime":1613992168196,
         "lastPx":"58501",
         "lastQty":"0.001",
         "orderId":"a177c29e4064U0123456789dVeUxlVyA",
         "orderQty":"0.001",
         "orderType":"Limit",
         "posStopLossPrice":"0",
         "posStopLossTrigger":"market",
         "posTakeProfitPrice":"0",
         "posTakeProfitTrigger":"market",
         "price":"59027",
         "seqNum":1041950,
         "side":"Buy",
         "status":"Filled",
         "stopBy":"market",
         "stopPrice":"0",
         "symbol":"BTC-PERP",
         "time":1613992168190
      },
      ...
   ]
}
```

This API returns all current history orders for futures account.

**HTTP Request**

`GET <account-group>/api/pro/v2/futures/order/hist/current`

**Prehash String**

`<timestamp>+v2/futures/order/hist/current`

**Request Parameters**

 Name            | Type      | Required | Description                                                                                 
---------------- | --------- | -------- | ------------------------------------------------------------------------------------------- 
 symbol          | String    | No       | symbol filter, e.g. `"BTC-PERP"`
 n               | Int       | No       | maximum number of orders to be included in the response
 executedOnly    | Boolean   | No       | if `True`, include orders with non-zero filled quantities only.

**Response**

Return a list of history orders in *"data"* field.
