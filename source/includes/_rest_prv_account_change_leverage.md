### Change Contract Leverage 

> Response

```json
{
    "code": 0,
    "data": {
        "leverage": 10,
        "symbol"  : "BTC-PERP"
    }
}
```

**HTTP Request**

`POST /<grp>/api/pro/v2/futures/leverage`



**Request Parameters**

PARAMETER | TYPE   | REQUIRED | DESCRIPTION
--------- |--------| -------- | ---------------
symbol    | String |  Yes     | e.g. `BTC-PERP`
leverage  | Int    |  Yes     | the leverage should be an integer between `1` and `100`
