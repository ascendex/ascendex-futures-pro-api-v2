### WS: Account Snapshot

> Requesting Futures Account Snapshot

```json
{
   "op"    : "req",
   "id"    : "abc123456",
   "action": "futures-account-snapshot"
}
```

> Futures Account Snapshot response

```json
{
   "m"  : "futures-account-snapshot",  // message
   "id" : "abc123456",                 // echo back the request Id
   "e"  : "ClientRequest",             // event name
   "t"  : 1613748277356,               // server time in milliseconds (UTC)
   "acc": "futH9N59hR0BMVEjHnBleHLn0mfUl5lo",  // accountId
   "ac" : "FUTURES",                   // account category
   "sn" : 9982,                        // sequence number
   "col":[  // collateral balances
      {
         "a": "ETH",     // collateral asset code
         "b": "500",     // collateral balance
         "f": "0.95"     // discount factor
      },
      {
         "a": "BTC",
         "b": "100",
         "f": "0.98"
      },
      {
         "a": "USDT",
         "b": "1000000",
         "f": "1"
      }
   ],
   "pos":[  // contract positions
      {
         "s"   : "BTC-PERP",  // contract symbol
         "sd"  : "NULL_VAL",  // side: LONG / SHORT / NULL_VAL
         "pos" : "0",         // position
         "rc"  : "0",         // reference cost
         "up"  : "0",         // unrealized pnl
         "rp"  : "0",         // realized pnl
         "aop" : "0",         // average opening price
         "mt"  : "crossed",   // margin type: isolated / cross
         "boon": "0",         // buy open order notional
         "soon": "0",         // sell open order notional
         "lev" : "10",        // leverage
         "iw"  : "0",         // isolated margin
         "tp"  : "0",         // take profit price (by position exit order)
         "tpt" : "market",    // take profit trigger (by position exit order)
         "sl"  : "0",         // stop loss price (by position exit order)
         "slt" : "market"     // stop loss trigger (by position exit order)
      }
   ]
}
```

You can request the futures account snapshot via websocket by a `futures-account-snapshot` action. 

The request schema:

 Name          | Data Type           | Description                
-------------- | ------------------- | -------------------------- 
 op            | String              | `req`                      
 action        | String              | `futures-account-snapshot`  
 id            | String              | for result match purpose       

