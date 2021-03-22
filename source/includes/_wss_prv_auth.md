### Authenticate a WebSocket Session

You must authenticate the websocket session in order to recieve private data and send account specific requests 
(e.g. placing new orders). 

You have two options to authenticate a websocket session. 

* by adding authentication data in the request header when connecting to websocket. 
* by sending an `op:auth` message to the server after you have connected to websocket. 

Once you successfully connect to the websocket, you will receive a `connected` message: 

* for authenticated websocket session: `{"op":"connected","type":"auth"}`
* for unauthenticated websocket session: `{"op":"connected","type":"unauth"}`

If the session is disconnected for some reason, you will receive a `disconnected` message:

* `{"m":"disconnected","code":100005,"reason":"INVALID_WS_REQUEST_DATA","info":"Session is disconnected due to missing pong message from the client"}`


### Prehash String

`<timestamp>+v2/stream`


### Method 1 - WebSocket Authentication with Request Headers

> Authenticate with Headers

```shell
# # Install wscat from Node.js if you haven't
# npm install -g wscat  

APIPATH=v2/stream
APIKEY=BclE7dBGbS1AP3VnOuq6s8fJH0fWbH7r
SECRET=fAZcQRUMxj3eX3DreIjFcPiJ9UR3ZTdgIw8mxddvtcDxLoXvdbXJuFQYadUUsF7q
TIMESTAMP=`date +%s%N | cut -c -13`
MESSAGE=$TIMESTAMP+$APIPATH
SIGNATURE=`echo -n $MESSAGE | openssl dgst -sha256 -hmac $SECRET -binary | base64`

wscat -H "x-auth-key: $APIKEY" \
  -H "x-auth-signature: $SIGNATURE" \
  -H "x-auth-timestamp: $TIMESTAMP" \
  -c wss://ascendex.com/1/api/pro/v2/stream -w 1 -x '{"op":"sub", "id": "abc123", "ch": "futures-order"}'
```

```python
# python 3.6+
import time, hashlib, hmac, base64
import asyncio    # pip3 install asyncio
import websockets # pip3 install websockets

def hashing(message: str, secret: str) -> str:
    msg = bytearray(message.encode("utf-8"))
    hmac_key = base64.b64decode(secret)
    signature = hmac.new(hmac_key, msg, hashlib.sha256)
    signature_b64 = base64.b64encode(signature.digest()).decode("utf-8")
    return signature_b64

def get_timestamp() -> int:
    return int(time.time() * 1000)


async def websocket_auth_demo(uri):
    apikey = "2pJkaH37i4wrVAMmFNoASVNCu4INP5F9"
    secret = "etvbsuZQafiECVdDb29PpwhzhWSf47kDpGxT8Fa7eZMjdGsUAQGHVudpt7S3ZY5w"
    ts = get_timestamp()
    message = str(ts) + "+v2/stream"
    sig = hashing(message, secret)
    auth_headers = [
        ("x-auth-key", apikey),
        ("x-auth-signature", sig),
        ("x-auth-timestamp", str(ts))]
    async with websockets.client.connect(uri, extra_headers=auth_headers) as websocket:
        while True:
            msg = await websocket.recv()
            print(msg)

asyncio.get_event_loop().run_until_complete(
    websocket_auth_demo('wss://ascendex.com:443/0/api/pro/v2/stream'))
```

```java
public static void main(String[] args) {
    System.out.println("Hello world");
}
```

This is similar to the way you authenticate any RESTful request. You need to add the following header fields to the 
connection request:

* `x-auth-key`
* `x-auth-timestamp`
* `x-auth-signature`

The server will then check if the data is correctly signed before upgrading the connection protocol to WebSocket. 

Note that if you specify these header fields, the server will reject the websocket connection request if authentication fails. 


### Method 2 - WebSocket Authentication by Sending the Auth Message 

> Authenticate by Sending the `auth` Message

```shell
# # Install wscat from Node.js if you haven't
# npm install -g wscat  

APIPATH=v2/stream
APIKEY=BclE7dBGbS1AP3VnOuq6s8fJH0fWbH7r
SECRET=fAZcQRUMxj3eX3DreIjFcPiJ9UR3ZTdgIw8mxddvtcDxLoXvdbXJuFQYadUUsF7q
TIMESTAMP=`date +%s%N | cut -c -13`
MESSAGE=$TIMESTAMP+$APIPATH
SIGNATURE=`echo -n $MESSAGE | openssl dgst -sha256 -hmac $SECRET -binary | base64`

wscat -c wss://ascendex.com/1/api/pro/v2/stream -w 1 -x "{\"op\":\"auth\", \"id\": \"abc123\", \"t\": $TIMESTAMP, "key": \"$APIKEY\", \"sig\": \"$SIGNATURE\"}"
```

```python
# python 3.6+
import json, time, hashlib, hmac, base64
import asyncio    # pip3 install asyncio
import websockets # pip3 install websockets

def hashing(message: str, secret: str) -> str:
    msg = bytearray(message.encode("utf-8"))
    hmac_key = base64.b64decode(secret)
    signature = hmac.new(hmac_key, msg, hashlib.sha256)
    signature_b64 = base64.b64encode(signature.digest()).decode("utf-8")
    return signature_b64

def get_timestamp() -> int:
    return int(time.time() * 1000)


async def websocket_auth_demo(uri):
    apikey = "2pJkaH37i4wrVAMmFNoASVNCu4INP5F9"
    secret = "etvbsuZQafiECVdDb29PpwhzhWSf47kDpGxT8Fa7eZMjdGsUAQGHVudpt7S3ZY5w"
    ts = get_timestamp()
    message = str(ts) + "+v2/stream"
    sig = hashing(message, secret)
    auth = dict(op="auth", id="RandomID123", t=ts, key=apikey, sig=sig)
    async with websockets.connect(uri) as websocket:
        await websocket.send(json.dumps(auth))
        while True:
            msg = await websocket.recv()
            print(msg)

asyncio.get_event_loop().run_until_complete(
    websocket_auth_demo('wss://ascendex.com:443/0/api/pro/v2/stream'))
```

```java
public static void main(String[] args) {
    System.out.println("Hello world");
}
```


You can also authenticate a live websocket session by sending an `op:auth` message to the server. 

 PARAMETER                      | TYPE       | REQUIRED | DESCRIPTION
------------------------------- | ---------- | -------- | ----------------------------------------------------------------------- 
 [op](#websocket-operations-op) |  ENUM      | Yes      | `"auth"`                                                                
 id                             |  String    | No       | optional id field, you may safely skip it                               
 t                              |  Long      | Yes      | UTC timestamp in milliseconds, use this timestamp to generate signature 
 key                            |  String    | Yes      | your api key
 sig                            |  String    | Yes      | the signature is generated by signing `"<timestamp>+v2/stream"`


### Authentication Response

> Auth success message

```json
{  
  "m": "auth",
  "id": "abc123",
  "code": 0
}
```

> Auth error message

```json
{
  "m":"auth",
  "id": "abc123",
  "code": 200006,
  "err": "Unable to find User Account Data"
}
```

You will receive a message for authentication result after you send authentication request.

PARAMETER | TYPE               | DESCRIPTION
--------- | ------------------ | ----------------------------------------------------------------------- 
m         |  ENUM              | `"auth"`
id        |  String            | echo back the id if you provide one in the request                      
code      |  Long              | Any code other than 0 indicate an error in authentication               
err       |  Optional[String]  | Provide detailed error message if code is not 0   
