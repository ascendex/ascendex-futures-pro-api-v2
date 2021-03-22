### Position

> Response

```json
{
    "code": 0,
    "data": {
        "ac"             : "FUTURES",                   // account category
        "accountId"      : "sample-futures-account-id", // account ID
        "collaterals": [
            {
                "asset"         : "ETH",          // collateral asset 
                "balance"       : "100",          // balance 
                "discountFactor": "0.95",         // discount factor
                "referencePrice": "481.79793092"  // reference price (quote in USDT)
            },
            {
                "asset"         : "BTC",
                "balance"       : "10",
                "discountFactor": "0.98",
                "referencePrice": "17600.095"
            },
            {
                "asset"         : "USDT",
                "balance"       : "10000",
                "discountFactor": "1",
                "referencePrice": "1"
            }
        ],
        "contracts": [
            {
                "symbol"               : "BTC-PERP",     // contract symbol
                "side"                 : "LONG",         // side
                "position"             : "0.5",          // positive for long position and negative for short position
                "referenceCost"        : "16800",        // reference cost
                "unrealizedPnl"        : "0",            // unrealized pnl 
                "realizedPnl"          : "0",            // realized pnl
                "avgOpenPrice"         : "0",            // Average Opening Price
                "marginType"           : "cross",        // margin type: isolated / cross
                "isolatedMargin"       : "0",            // isolated margin
                "leverage"             : "10",           // leverage
                "takeProfitPrice"      : "0",            // take profit price (by position exit order)
                "takeProfitTrigger"    : "market",       // take profit trigger (by position exit order)
                "stopLossPrice"        : "0",            // stop loss price (by position exit order)
                "stopLossTrigger"      : "market",       // stop loss trigger (by position exit order)
                "buyOpenOrderNotional" : "1362.419625",  // buy open order notional
                "sellOpenOrderNotional": "0",            // sell open order notional
                "indexPrice"           : "17600.095",    // price of the contract's underlying product price
                "markPrice"            : "-1"            // contract's mark price
            }
        ]
    }
}
```

Get current position data - a full snapshot of your futures account. 

**HTTP Request**

`GET /<grp>/api/pro/v2/futures/position`

**Prehash String**

`<timestamp>+v2/futures/position`


