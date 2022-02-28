### Exchange Risk Limit Info

> Risk Limit Info

```
curl -X GET https://ascendex.com/api/pro/v1/risk-limit-info"
```

> Risk Limit Info - Sample response::

```json
{
  "code": 0,
  "data": {
    "ip": "0.0.0.0",
    "webSocket": {
      "windowSizeInMinutes": 5,
      "maxNumRequests": 45,
      "maxSessionPerIp": 30,
      "isBanned": true,
      "bannedUntil": 1644807691158,
      "violationCode": 100014,
      "reason": "exceeds MAX_REQ_COUNT_PER_IP[45], 49 requests recently"
    }
  }
}
```

**HTTP Request**

`GET /api/pro/v1/exchange-info`

#### Request Parameters

Name        |  Type    | Required | Value Range                                    | Description
----------- | -------- | -------- | -----------------------------------------------|---------------
ip          |  String  |   No     | valid ip address | the client's ip address to be checked if it is banned due to violation of risk limits.


