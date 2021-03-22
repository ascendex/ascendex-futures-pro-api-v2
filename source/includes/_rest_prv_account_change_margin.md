### Change Margin (for Isolated Positions)

> Successful Response

```json
{
    "code": 0
}
```

You can only change margin for isolated margin positions.

See [Free Margin](#free-margin) on the maximum amount you can increase / decrease the isolated margin.

**HTTP Request**

`POST /<grp>/api/pro/v2/futures/isolated-position-margin`

**Prehash String**

`<timestamp>+v2/futures/isolated-position-margin`


**Request Parameters**

PARAMETER  | TYPE   | REQUIRED | DESCRIPTION
---------- |--------| -------- | ---------------
symbol     | String |  Yes     | e.g. `BTC-PERP`
amount     | String |  Yes     | margin amount in string type, e.g. "100". Set `amount` to positive will increase the isolated margin; set `amount` 
to a negative number will decrease the isolated margin. 


When you increase/decrease the isolated margin by a certain amount, the same amount X will be deducted/added from your USDT balance in the collateral. 

When you have non-USDT collateral assets, you may be able to increase the isolated margin by an amount more than your USDT balance. 
In which case, your USDT balance will become negative after the operation. 
