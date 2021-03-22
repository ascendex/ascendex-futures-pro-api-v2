### Channel: Market Trades

> Subscribe to `BTC-PERP` market trades stream

```json
{ "op": "sub", "id": "abc123", "ch":"trades:BTC-PERP" }
```

> Unsubscribe to `BTC-PERP` market trades stream

```json
{ "op": "unsub", "id": "abc123", "ch":"trades:BTC-PERP" }
```

> Trade Message 

```json
{
    "m": "trades",
    "symbol": "BTC-PERP",
    "data": [
        {
            "p":      "0.068600",
            "q":      "100.000",
            "ts":      1573069903254,
            "bm":      false,
            "seqnum":  144115188077966308
        }
    ]
}
```

The `data` field is a list containing one or more trade objects. The server may combine consecutive trades with the same price and `bm` 
value into one aggregated item. Each trade object contains the following fields:

 Name     | Type       | Description                                                                                    
--------- | ---------- | ---------------------------------------------------------------------------------------------- 
 seqnum   | Long       | the sequence number of the trade record. `seqnum` is always increasing for each symbol, but may not be consecutive 
 p        | String     | the executed price expressed as a string                                                       
 q        | String     | the aggregated traded amount expressed as string                                               
 ts       | Long       | the UTC timestamp in milliseconds of the first trade                                           
 bm       | Boolean    | if true, the buyer of the trade is the maker.                