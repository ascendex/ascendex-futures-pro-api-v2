### Deposit to the Futures Account


> Successful Response

```json
{
    "code": 0
}
```

You can deposit collateral assets to your Futures account from your Cash account.

**HTTP Request**

`POST /<grp>/api/pro/v2/futures/transfer/deposit`

**Prehash String**

`<timestamp>+v2/futures/transfer/deposit`

**Request Parameters**

PARAMETER  | TYPE   | REQUIRED | DESCRIPTION
---------- |--------| -------- | ---------------
asset      | String |  Yes     | e.g. `BTC`
amount     | String |  Yes     | the amount to deposit in string type, e.g. "1". Only positive value is allowed.




### Withdraw from the Futures Account

> Successful Response

```json
{
    "code": 0
}
```

You can withdraw collateral assets from your Futures account to your Cash account.

**HTTP Request**

`POST /<grp>/api/pro/v2/futures/transfer/withdraw`

**Prehash String**

`<timestamp>+v2/futures/transfer/withdraw`

**Request Parameters**

PARAMETER  | TYPE   | REQUIRED | DESCRIPTION
---------- |--------| -------- | ---------------
asset      | String |  Yes     | e.g. `BTC`
amount     | String |  Yes     | the amount to withdraw in string type, e.g. "1". Only positive value is allowed.

