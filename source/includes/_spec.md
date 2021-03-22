# General Info


## Futures Trading System Specification


### Contract Position Notional (CPN)

* CPN = abs(position size * mark price) for the contract 

CPN is defined for each contract.


### Total Margin

**For the isolated group**

Total margin is set by the user. You can find its value in the `isolatedMargin` field from the [Position](#position) endpoint. 

You can increase / decrease the total margin of the isolated margin group via the [Change Margin](#change-margin-for-isolated-positions) endpoint.


**For the crossed group**

* Total Margin = sum(Asset Balance * Reference Price * Collateral Discount Factor) for each collateral asset

Discount factor can be found in the `discountFactor` field from the [Futures Collateral Asset Info](#futures-collateral-asset-info) endpoint.



### Position Initial/Maintenance Margin Rate

Initial/Maintenance Margin Rate is system-specified for each position bracket and each contract. You may refer to the `marginRequirements` 
section from the [Futures Contract Info](#futures-contracts-info) endpoint for position brackets.

You should compare [Contract Position Notional (CPN)](#contract-position-notional-cpn) with each position bracket to determine your initial and 
maintenance margin rate.



### Position Initial/Maintenance Margin

**For the isolated group**

* Position Initial Margin = CPN * Initial Margin Rate
* Position Maintenance Margin = CPN * Maintenance Margin

**For the crossed group**

* Position Initial Margin = sum(CPN * Initial Margin Rate) for each contract in the crossed group
* Position Maintenance Margin = sum(CPN * Maintenance Margin) Rate for each contract in the crossed group



### Liquidation Price

* V = Total Margin + Unrealized Pnl - Maintenance Margin

**For long positions**

* R = abs(position size) * (1 - maintenance margin rate)
* Liquidation Price = mark price - V / R

If the calculated liquidation price is negative, the position won't be liquidation even when the price becomes zero.


**For short positions**

* R = abs(position size) * (1 + maintenance margin rate)
* Liquidation Price = mark price + V / R
