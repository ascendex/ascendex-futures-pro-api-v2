### Channel: Order

```json
{
  "m"      : "futures-order",
  "sn"     : 127,                   // sequence number
  "e"      : "ExecutionReport",     // event
  "a"      : "sample-futures-account-id",  // account Id
  "ac"     : "FUTURES",             // account category 
  "t"      : 1606335352348,         // last execution time
  "ct"     : 1606335351541,         // order creation time
  "orderId": "a176010c4957U68469127074abcd1234",  // order Id
  "sd"     : "Buy",                 // side 
  "ot"     : "Limit",               // order type 
  "q"      : "0.1",                 // order quantity (base asset)
  "p"      : "18000",               // order price
  "sp"     : "0",                   // stop price
  "spb"    : "",                    // stop trigger
  "s"      : "BTC-PERP",            // symbol 
  "st"     : "New",                 // order status
  "lp"     : "0",                   // last filled price
  "lq"     : "0",                   // last filled quantity (base asset)
  "ap"     : "0",                   // average filled price
  "cfq"    : "0",                   // cummulative filled quantity (base asset)
  "f"      : "0",                   // commission fee of the current execution
  "cf"     : "0",                   // cumulative commission fee
  "fa"     : "USDT",                // fee asset
  "ei"     : "NULL_VAL",            // execution instruction
  "err"    : ""                     // error message
}
```

**Subscribe to the Channel**

`{"op":"sub", "id":"sample-id", "ch":"futures-order"}`

