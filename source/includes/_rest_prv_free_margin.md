### Free Margin

> Response

```json
{
  "code": 0,
  "data": {
    "collaterals": [
      {
        "asset": "BTC",              // collateral asset
        "availableForTransfer": "1"  // maximum amount allowed to be transferred out
      },
      {
        "asset": "USDT",
        "availableForTransfer": "10000"
      }
    ],
    "crossed": {
      "freeMargin": "30000"
    },
    "isolated": [
      {
        "freeMargin": "0",
        "symbol": "BTC-PERP"
      }
    ]
  }
}
```

Get free margin for each margin group (crossed & isolated) and amount avaible for withdrawal for each collateral asset.

See [Change Margin](#change-margin-for-isolated-positions) on how to increase or decrease margin for the isolated position.

![change-isolated-margin](../images/change-isolated-margin.png)

**HTTP Request**

`GET /<grp>/api/pro/v2/futures/free-margin`

**Prehash String**

`<timestamp>+v2/futures/free-margin`

