### Funding Payment History

> Response

```json
{
  "code": 0,
  "data": {
    "data": [
      {
        "fundingRate": "0.00003666",
        "paymentInUSDT": "-0.000142423",
        "symbol": "BTC-PERP",
        "timestamp": 1642780800000
      },
      {
        "fundingRate": "0.000109429",
        "paymentInUSDT": "-0.000428031",
        "symbol": "BTC-PERP",
        "timestamp": 1642752000000
      }
    ],
    "hasNext": true,
    "page": 1,
    "pageSize": 2
  }
}
```

Get funding payment history of your account. 

**HTTP Request**

`GET /<grp>/api/pro/v2/futures/funding-payments`

**Prehash String**

`<timestamp>+v2/futures/funding-payments`

**Request Parameters**

Name       | Type   | Required | Description
---------- | ------ | -------- | ---------------------------------------------
`symbol`   | String | No       | e.g. `BTCUSDT`
`page`     | Int    | No       | page number, default 1
`pageSize` | Int    | No       | size of the page, 1~100, default 20.


**Code Sample**

Please refer to python code to [get funding history](https://github.com/ascendex/ascendex-futures-api-demo-v2/blob/main/cli/get-funding-history.py)
