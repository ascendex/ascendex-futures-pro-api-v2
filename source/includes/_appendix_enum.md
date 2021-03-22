## ENUM Definitions

### Account Category (`ac`)

* `CASH`
* `MARGIN`
* `FUTURES`

### Order Type (`orderType`)

* `Limit`
* `Market`
* `StopLimit`
* `StopMarket`

### Side (`side`)

* `Buy`
* `Sell`

### Response Type (`respInst`)

* `ACK`
* `ACCEPT`
* `DONE`

### Time in Force (`timeInForce`)

* `GTC` - good till cancelled 
* `IOC` - immediate or cancel
* `FOK` - fill or kill

### Execution Instruction (`execInst`)

* `Post`
* `Liquidation`
* `InternalPost`
* `StopOnMarket`
* `StopOnMark`
* `StopOnRef`
* `ReduceOnly`
* `PostReduceOnly`
* `PostStopMarket`
* `PostStopMark`
* `PostStopRef`
* `ReduceOnlyMarket`
* `ReduceOnlyMark`
* `ReduceOnlyRef`
* `PostReduceMarket`
* `PostReduceMark`
* `PostReduceRef`
* `OpenStopMkt`
* `OpenStopMark`
* `OpenStopRef`
* `OpenPostStopMkt`
* `OpenPostStopMark`
* `OpenPostStopRef`
* `PosStopMkt`
* `PosStopMark`
* `PosStopRef`

### Margin Type (`marginType`)

* `crossed`
* `isolated`

### WebSocket Operations (`op`)

* `auth`

### WebSocket Message Types (`m`)

* `auth`
* `sub`
* `unsub`
* `bbo`
* `futures-pricing-data-batch`
* `futures-order`
* `futures-account-update`

