### Channel: Futures Pricing Data

> Sample Futures Pricing Data Message

```json
{
    "m": "futures-pricing-data",
    "con": [  // contracts
        {
            "s" : "BTC-PERP",        // symbol
            "t" : 1614814705716,     // data time
            "ip": "50702.8",         // index price
            "mp": "50652.3553",      // mark price
            "r" : "0.000565699",     // funding rate 
            "oi": "90.7367",         // open interest
            "f" : 1614816000000      // next funding time
        }
    ], 
    "col": [  // collateral assets
        {
            "a": "USDTR",  // asset
            "p": "1"       // reference price (quote in USDT)
        },
        {
            "a": "USDC",
            "p": "0.99935"
        },
        {
            "a": "ETH",
            "p": "1582.505"
        },
        {
            "a": "PAX",
            "p": "0.9964"
        },
        {
            "a": "BTC",
            "p": "50621.795"
        },
        {
            "a": "USDT",
            "p": "1"
        }
    ]
}
```


**Subscribe to the Channel**

`{"op":"sub", "id":"sample-id", "ch":"futures-pricing-data"}`

