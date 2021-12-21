### Exchange Latency Info

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

`GET /api/pro/v1/exchange-info?requestTime="$(date +%s%N | cut -b1-13)"`