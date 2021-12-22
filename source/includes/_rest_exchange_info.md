### Exchange Latency Info

> Latency Info 

```
curl -X GET https://ascendex.com/api/pro/v1/exchange-info?requestTime="$(date +%s%N | cut -b1-13)"
```

> Latency Info - Sample response::

```json
{
    "code": 0,
    "data":
    {
        "requestTimeEcho": 1640052379050,
        "requestReceiveAt": 1640052379063,
        "latency": 13
    }
}
```

**HTTP Request** 

`GET /api/pro/v1/exchange-info`

#### Request Parameters

Name        |  Type    | Required | Value Range                                    | Description
----------- | -------- | -------- | -----------------------------------------------|---------------
requestTime |  Long    |   Yes    | milliseconds since UNIX epoch in UTC | the client's local time. The server compare it with the system time to calculate latency.


