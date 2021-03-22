### Futures Pricing Data


> Requesting pricing data for all futures contract

```json
{
    "code": 0,
    "data": {
        "contracts": [
            {
                "symbol"         : "BTC-PERP",          // contract symbol
                "time"           : 1614815005717,       // server time (UTC timestamp in milliseconds)
                "fundingRate"    : "0.000564448",       // funding rate 
                "indexPrice"     : "50657.35",          // index price of the underlying
                "markPrice"      : "50667.130409723",   // mark price of the contract
                "openInterest"   : "90.7366",           // funding rate
                "nextFundingTime": 1614816000000        // next funding time (UTC timestamp in milliseconds)
            }
        ],
        "collaterals": [
            {
                "asset": "USDTR",
                "referencePrice": "1"
            },
            {
                "asset": "USDC",
                "referencePrice": "0.9994"
            },
            {
                "asset": "ETH",
                "referencePrice": "1582.3264074"
            },
            {
                "asset": "PAX",
                "referencePrice": "0.99645"
            },
            {
                "asset": "BTC",
                "referencePrice": "50636.14"
            },
            {
                "asset": "USDT",
                "referencePrice": "1"
            }
        ],
    }
}
```

Get pricing data for all futures contracts. 

**HTTP Request**

`GET /api/pro/v2/futures/pricing-data`

