### Risk Limit Info (v2)

> Risk Limit Info v2

Our message thresholds in web socket are based on `op` field and `action` field.  Each threshold will have two levels, which are based on counts of messages received in `1` minute. If level 1 threshold is violated, this type of messages will be ignored in the following 15 minutes, other functions are not affected. If you keep sending these messages and triggered level 2 threshold, the violated WebSocket session will be killed and this ip will be banned for 15 minutes. Currently, We have following threshold groups:

- `admin op`, includes `auth/ping/pong`

- `stream op`, includes `sub/unsub`

- `req op`, includes all `req` op, but `order req` and `snapshot req` have their own thresholds

  - `order req`, includes `place_order/cancel_order/cancel_all`

  - `snapshot req`, includes `depth_snapshot/depth_snapshot_top100`

All the operations fall into same `op`/`req` group will share a threshold, meaning the sum of count of these messages should not violate the threshold.

For `req op`, we have two fine granularity threshold `order req` and `snapshot req`, which will have their specialized threshold value for messages belonging to their types.

```
curl -X GET https://ascendex.com/api/pro/v2/risk-limit-info"
```

> Risk Limit Info - Sample response::

```json
{
  "code": 0,
  "data": {
    "ip": "173.123.133.23",
    "webSocket": {
      "status": {
        "isBanned": false,
        "bannedUntil": -1,
        "violationCode": 0,
        "reason": ""
      },
      "limits": {
        "maxWebSocketSessionsPerIpAccountGroup": 20,
        "maxWebSocketSessionsPerIpTotal": 300
      },
      "messageThreshold": {
        "level1OpThreshold": {
          "auth": 800,
          "ping": 800,
          "pong": 800,
          "sub": 150,
          "unsub": 150,
          "req": 10000
        },
        "level2OpThreshold": {
          "auth": 1000,
          "ping": 1000,
          "pong": 1000,
          "sub": 200,
          "unsub": 200,
          "req": 10000
        },
        "level1ReqThreshold": {
          "place_order": 8000,
          "cancel_order": 8000,
          "cancel_all": 8000,
          "batch_place_order": 10000,
          "batch_cancel_order": 10000,
          "depth_snapshot": 400,
          "depth_snapshot_top100": 400,
          "market_trades": 10000,
          "balance": 10000,
          "open_order": 10000,
          "margin_risk": 10000,
          "futures_account_snapshot": 10000,
          "futures_open_orders": 10000
        },
        "level2ReqThreshold": {
          "place_order": 10000,
          "cancel_order": 10000,
          "cancel_all": 10000,
          "batch_place_order": 10000,
          "batch_cancel_order": 10000,
          "depth_snapshot": 500,
          "depth_snapshot_top100": 500,
          "market_trades": 10000,
          "balance": 10000,
          "open_order": 10000,
          "margin_risk": 10000,
          "futures_account_snapshot": 10000,
          "futures_open_orders": 10000
        }
      }
    }
  }
}
```

**HTTP Request**

`GET /api/pro/v2/risk-limit-info`

#### Request Parameters

Name        |  Type    | Required | Value Range                                    | Description
----------- | -------- | -------- | -----------------------------------------------|---------------
ip          |  String  |   No     | valid ip address | the client's ip address to be checked if it is banned due to violation of risk limits.


