### Ticker

> Ticker for one trading pair

```json
// curl -X GET 'https://ascendex.com/api/pro/v2/futures/ticker?symbol=BTC-PERP'
{
    "code": 0,
    "data":
    {
        "symbol":  "BTC-PERP",
        "open":    "59488",
        "close":   "56725",
        "high":    "59724",
        "low":     "56672",
        "baseVol": "208.7414",
        "ask":
        [
            "56730",
            "0.0005"
        ],
        "bid":
        [
            "56710",
            "0.0042"
        ]
    }
}
```

> List of Tickers for one or multiple trading pairs

```json
// curl -X GET "https://ascendex.com/api/pro/v2/futures/ticker?symbol=BTC-PERP,"
{
    "code": 0,
    "data":
    [
        {
            "symbol":  "BTC-PERP",
            "open":    "59488",
            "close":   "56716",
            "high":    "59724",
            "low":     "56672",
            "baseVol": "208.7414",
            "ask":
            [
                "56720",
                "0.2315"
            ],
            "bid":
            [
                "56712",
                "0.0024"
            ]
        }
    ]
}
```

#### HTTP Request

`GET api/pro/v2/futures/ticker`

You can get summary statistics of one or multiple symbols (spot market) with this API. 

#### Request Parameters

Name       | Type      | Required | Value Range | Description
-----------| --------- | -------- | ----------- | ---------------
`symbol`   | `String`  |  No      |             | you may specify one, multiple, or all symbols of interest. See below.


This API endpoint accepts one optional string field `symbol`: 

* If you do not specify `symbol`, the API will responde with tickers of all symbols in a list. 
* If you set `symbol` to be a single symbol, such as `ASD/USDT`, the API will respond with the ticker of the target symbol as an object. 
  If you want to wrap the object in a one-element list, append a comma to the symbol, e.g. `ASD/USDT,`.
* You shall specify `symbol` as a comma separated symbol list, e.g. `ASD/USDT,BTC/USDT`. The API will respond with a list of tickers. 

#### Respond Content

The API will respond with a ticker object or a list of ticker objects, depending on how you set the `symbol` parameter. 

Each ticker object contains the following fields:

 Field      | Type                 | Description                                                                                 
----------- | -------------------- | --------------------- 
 `symbol`   |  `String`            | 
 `open`     |  `String`            | the traded price 24 hour ago
 `close`    |  `String`            | the last traded price
 `high`     |  `String`            | the highest price over the past 24 hours 
 `low`      |  `String`            | the lowest price over the past 24 hours 
 `volume`   |  `String`            | the total traded volume in quote asset over the paste 24 hours
 `ask`      |  `[String, String]`  | the price and size at the current best ask level
 `bid`      |  `[String, String]`  | the price and size at the current best bid level

#### Code Sample

Please refer to python code to [query ticker info]{https://github.com/ascendex/ascendex-pro-api-demo/blob/main/python/query_pub_ticker.py}
