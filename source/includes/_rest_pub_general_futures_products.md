### Futures Contracts Info

> Response - Futures Contracts Info

```json
{
    "code": 0,
    "data": [
        {
            "symbol"          : "BTC-PERP",
            "status"          : "Normal",
            "displayName"     : "BTCUSDT",    // the name displayed on the webpage
            "settlementAsset" : "USDT",       // settlement asset
            "underlying"      : "BTC/USDT",
            "tradingStartTime": 1579701600000,
            "priceFilter": {
                "minPrice"  : "0.25",     // the order price cannot be smaller than the minPrice
                "maxPrice"  : "1000000",  // the order price cannot be greater than the maxPrice
                "tickSize"  : "0.25"      // the order price must be a multiple of the tickSize
            },
            "lotSizeFilter": {
                "minQty"  : "0.0001",     // the order quantity cannot be smaller than the minQty
                "maxQty"  : "1000000000", // the order quantity cannot be greater than the maxQty
                "lotSize" : "0.0001"      // the order quantity must be a multiple of the lotSize
            },
            "marginRequirements": [
                {
                    "positionNotionalLowerbound": "0",     // position lower bound
                    "positionNotionalUpperbound": "50000", // position upper bound
                    "initialMarginRate"         : "0.01",  // initial margin rate
                    "maintenanceMarginRate"     : "0.006"  // maintenance margin rate
                },
                {
                    "positionNotionalLowerbound": "50000",
                    "positionNotionalUpperbound": "200000",
                    "initialMarginRate"         : "0.02",
                    "maintenanceMarginRate"     : "0.012"
                }
            ]
        }
    ]
}
```

Get information for all futures contracts.

**HTTP Request**

`GET /api/pro/v2/futures/contract`

**Response**




### Futures Collateral Asset Info

> Response - Futures Collateral Asset Info

```json
{
    "code": 0,
    "data": [
        {
            "asset"           : "BTC",
            "assetName"       : "Bitcoin",
            "conversionFactor": "0.995",
            "discountFactor"  : "0.98",
            "displayName"     : "BTC",
            "statusCode"      : "Normal"
        },
        {
            "asset"           : "USDT",
            "assetName"       : "Tether",
            "conversionFactor": "1",
            "discountFactor"  : "1",
            "displayName"     : "USDT",
            "statusCode"      : "Normal"
        },
        {
            "asset"           : "USDTR",
            "assetName"       : "Futures Reward Token",
            "conversionFactor": "1",
            "discountFactor"  : "1",
            "displayName"     : "USDTR",
            "statusCode"      : "NoTransaction"
        }
    ]
}
```

Get information for all futures collateral assets.

**HTTP Request**

`GET /api/pro/v2/futures/collateral`
