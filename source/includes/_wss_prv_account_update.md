### Channel: Account Update

```json


{
  "m"     : "futures-account-update",            // message
  "e"     : "ExecutionReport",                   // event type
  "t"     : 1612508562129,                       // server time (UTC time in milliseconds)
  "acc"   : "sample-futures-account-id",         // account ID
  "at"    : "FUTURES",                           // account type
  "sn"    : 23128,                               // sequence number, strictly increasing for each account
  "id"    : "r177710001cbU3813942147C5kbFGOan",  // request ID for this account update
  "col": [
    {
      "a": "USDT",               // asset code
      "b": "1000000",            // balance 
      "f": "1"                   // discount factor
    }
  ],
  "pos": [
    {
      "s"   : "BTC-PERP",        // symbol
      "sd"  : "LONG",            // side
      "pos" : "0.011",           // position
      "rc"  : "-385.840455",     // reference cost
      "up"  : "18.436008668",    // unrealized pnl
      "rp"  : "0",               // realized pnl
      "aop" : "35041.363636363", // Average Opening Price
      "boon": "0",               // Buy Open Order Notional
      "soon": "0",               // Sell Open Order Notional
      "mt"  : "crossed",         // margin type: isolated / cross
      "iw"  : "0",               // isolated margin
      "lev" : "10",              // leverage
      "tp"  : "0",               // take profit price (by position exit order)
      "tpt" : "market",          // take profit trigger (by position exit order)
      "sl"  : "0",               // stop loss price (by position exit order)
      "slt" : "market",          // stop loss trigger (by position exit order)
    }
  ]
}
```


**Subscribe to the Channel**

`{"op":"sub", "id":"sample-id", "ch":"futures-account-update"}`



