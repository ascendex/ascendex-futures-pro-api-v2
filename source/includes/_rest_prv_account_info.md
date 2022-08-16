### Account Info

> Account Info - Sample response:

```json
{
    "code": 0,
    "data": {
        "accountGroup": 0,
        "email": "yyzzxxz@gmail.com",
        "expireTime": 1604620800000,         // expire time, UTC timestamp in milliseconds. If -1, the api key will not expire
        "allowedIps": ["123.123.123.123"],
        "cashAccount": [
            "sample-cash-account-id"
        ],
        "marginAccount": [
            "sample-margin-account-id"
        ],
        "futuresAccount": [
            "sample-futures-account-id"
        ],
        "userUID":            "U0866943712",
        "tradePermission":     true,
        "transferPermission":  true,
        "viewPermission":      true,
        "limitQuota":          1000
    }
}
```

**HTTP Request** 

`GET /api/pro/v2/account/info`

**Signature**

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-a-request) section.

**prehash string** 

`<timestamp>+v2/account/info`

Obtain the account information. 

You can obtain your `accountGroup` from this API, which you will need to include in the URL for all your private RESTful requests.

#### Response Content

 Name              | Type         | Description
------------------ | ------------ | --------------------- 
accountGroup       | Int          | non-negative integer
email              | String       | 
expireTime         | Long         | the time when the API key will be expired (UTC timestamp in milliseconds). If -1, the api key will not expire
allowedIps         | List[String] | list of IPs allowed for the api key
cashAccount        | List[String] | 
marginAccount      | List[String] | 
tradePermission    | Boolean      | 
transferPermission | Boolean      | 
viewPermission     | Boolean      | 
userUID            | String       | an unique id associated with user

See a demo at [query private account info](https://github.com/ascendex/ascendex-pro-api-demo/blob/main/python/query_prv_account_info.py).

