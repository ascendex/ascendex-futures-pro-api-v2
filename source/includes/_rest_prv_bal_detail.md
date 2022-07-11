## Balance Snapshot And Update Detail

Here we provide rest API to get daily balance snapshot, and intraday balance and order fills update details. We recommend calling balance snapshot endpoint(`futures/balance/snapshot`) to get balance at the beginning of the day, and get the sequence number `sn`; then start to query balance or order fills update from `futures/balance/history` by setting parameter `sn` value to be `sn + 1`.

Please note we enforce rate limit 8 / minute. Data query for most recent 7 days is supported.

### Futures Account Balance Snapshot

This API returns futures balance snapshot on daily basis.

#### HTTP Request

`GET  api/pro/data/v1/futures/balance/snapshot`

#### Signature

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#signing-a-Request) section.

#### Prehash String

`<timestamp>+data/v1/futures/balance/snapshot`

#### Request Parameters

Name        |  Type     | Required |           Value Range       | Description
------------| --------- | -------- |-----------------------------| -----------
**date**    | `String`  |   Yes    | `YYYY-mm-dd`                |  balance date

#### Response Content

 Name                | Type         | Description
-------------------- | -------------| ---------------------------------
**meta**             | `Json`       | `meta` info. See detail below
**collateralBalance**| `Json Array` | `collateral balance` info. See detail below
**contractBalance**  | `Json Array` | `contract balance` info. See detail below

`meta` field provides some basic info about the balance snapshot data.

`meta` schema

 Name          | Type     | Description                           | Sample Response
---------------| -------- | --------------------------------------|-------------------------
**ac**         | `String` | account category                      | `"futures`
**accountId**  | `String` | accountId                             |
**sn**         | `Long`   | sequence number                       |
**balanceTime**| `Long`   | balance snapshot time in milli seconds|

`collateralBalance` field provides array of ‘asset’ and ‘totalBalance’ for collateral balance.

`collateralBalance` schema

 Name              | Type     | Description                   | Sample Response
-------------------| -------- | ------------------------------| ----------------
**asset**          | `String` | asset code                    | `"USDT"`
**totalBalance**   | `String` | current asset total balance   | `"1234.56"`

`contractBalance` field provides array of current contract positions infomation.

`contractBalance` schema

 Name                  | Type     | Description               |Sample Response
-----------------------| -------- | --------------------------| ----------------
**contract**           | `String` | contract name             | `"USDT"`
**futuresAssetBalance**| `String` | current contract position | `"1234.56"`
**isolatedMargin**     | `String` | Isolated margin           | `"134.56"`
**refCostBalance**     | `String` | Reference cost            | `"34.56"`

#### Code Sample

Please refer to python code to [query balance snapshot](https://github.com/ascendex/ascendex-pro-api-demo/blob/master/python/query_balance_and_order_fills.py)


### Futures Order and Balance Detail

This API is for intraday balance change detail from balance event and order fillss.

#### HTTP Request

`GET  api/pro/data/v1/futures/balance/history`

#### Prehash String

`<timestamp>+data/v1/futures/balance/history`

> Futures Account Balance Detail - Sample response

```json
{
    "balance": [
        {
            "data": [
                {
                    "asset": "XPRTPC",
                    "curBalance": "-7.873230189",
                    "deltaQty": "0.004117158"
                }
            ],
            "eventType": "Fundingpayment",
            "sn": 18591022051,
            "transactTime": 1634947227877
        },
        {
            "data": [
                {
                    "asset": "BTCPC",
                    "curBalance": "-307.654491085",
                    "deltaQty": "10.673854479"
                },
                {
                    "asset": "USDT",
                    "curBalance": "149.493187792",
                    "deltaQty": "10.673854479"
                }
            ],
            "eventType": "Futuressettlement",
            "sn": 18590550015,
            "transactTime": 1634913817331
        }
    ],
    "meta": {
        "ac": "futures",
        "accountId": "futfi7p9j312936d2hkjJpAahWyb4RCJ"
    },
    "order": [
        {
            "data": [
                {
                    "asset": "PORTP",
                    "curBalance": "1",
                    "dataType": "trade",
                    "deltaQty": "1"
                },
                {
                    "asset": "PORTPC",
                    "curBalance": "-6.213726",
                    "dataType": "trade",
                    "deltaQty": "-6.21"
                },
                {
                    "asset": "PORTPC",
                    "curBalance": "-6.213726",
                    "dataType": "fee",
                    "deltaQty": "-0.003726"
                }
            ],
            "liquidityInd": "RemovedLiquidity",
            "orderId": "r17ca5840c64U7684578612bportL84r",
            "orderType": "Market",
            "side": "Buy",
            "sn": 18589783182,
            "transactTime": 1634864467246
        }
    ]
}
```


#### Request Parameters

Name           |  Type     | Required |           Value Range         | Description
-------------- | --------- | -------- | ------------------------------| -----------
**sn**         | `Long`    |   Yes    |  start from snapshot `sn`     | Start sn 
**limit**      | `Int`     |   No     |  1 to 500                     | Number of records. max 500 


#### Response Content

 Name       | Type         | Description
----------- | -------------| ---------------------------------
**meta**    | `Json`       | `meta` info. See detail below
**order**   | `Json Array` | `order` info. See detail below
**balance** | `Json Array` | `balance` info. See detail below

##### Meta 
`meta` field provides some basic info.

`meta` schema

 Name                | Type     | Description      | Sample Response
-------------------- | -------- | -----------------| -------------------------
**ac**               | `String` | account category | `"cash", "margin", "futures`
**accountId**        | `String` | accountId        | 

##### Order

`order` field provides an array of asset balance detail from order fill event.

`order` schema

 Name            | Type        | Description                    | Sample Response
-----------------| ----------- | -------------------------------| -------------------------
**liquidityInd** | `String`    | liquidity indicator            | `RemovedLiquidity` for taker order, `AddedLiquidity` for maker order, or `NULL_VAL`
**orderId**      | `String`    | orderId                        | order Id
**orderType**    | `String`    | order type                     | `market`, `limit`
**side**         | `String`    | order side                     | `buy`, `sell`
**sn**           | `Long`      | sequence number                | unique and increasing sequence number
**transactTime** | `Long`      | transactTime in milli seconds  |
**data**         | `Json Array`| list of order info json objects| see detail below

order balance detail by asset

`data` schema

 Name                | Type     | Description                                           | Sample Response
-------------------- | -------- | ----------------------------------------------------- | ----------------
**asset**            | `String` | asset code                                            | `"USDT"`
**curBalance**       | `String` | asset balance after this transaction                  | `"1234.56"`
**dataType**         | `String` | `trade` for trading asset; `fee` for fee balance asset| `trade`, `fee`
**deltaQty**         | `String` | balance change in this transaction                    | `100`

##### Balance

`balance` field provides an array of asset balance detail due to balance event.

`balance` schema

 Name            | Type        | Description                      | Sample Response
-----------------| ----------- | ---------------------------------| -----------------------
**eventType**    | `String`    | balance event type               | `deposit`, `withdrawal`
**sn**           | `Long`      | sequence number                  |
**transactTime** | `Long`      | transactTime in milli seconds    |
**data**         | `Json Array`| list of balance info json objects| see detail below

`data` schema

 Name                | Type     | Description                                           | Sample Response
-------------------- | -------- | ----------------------------------------------------- | ----------------
**asset**            | `String` | asset code                                            | `"USDT"`
**curBalance**       | `String` | asset balance after this transaction                  | `"1234.56"`
**deltaQty**         | `String` | balance change in this transaction                    | `100`


#### Code Sample

Please refer to python code to [query order and balance detail](https://github.com/ascendex/ascendex-pro-api-demo/blob/master/python/query_balance_and_order_fills.py)
