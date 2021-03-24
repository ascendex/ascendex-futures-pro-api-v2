# General Info


## Futures Trading System Specification


### Contract Position Notional (CPN)

* CPN = abs(position size * mark price) for the contract 

CPN is defined for each contract.


### Margin Group 

**The Isolated Group**

The isolated group manages a single position with a certain amount of margin moved out of the crossed group. It isolates the risk of the position from other 
margin groups. Your maximum loss will be limited to the total margin moved into the isolated group.

Each account may have at most one isolated group per contract.

**The Crossed Group**

The crossed group manages all positions except those in isolated groups. 


### Total Margin

**For the isolated group**

Total margin is set by the user. You can find its value in the `isolatedMargin` field from the [Position](#position) endpoint. 

You can increase / decrease the total margin of the isolated margin group via the [Change Margin](#change-margin-for-isolated-positions) endpoint.

For the isolated group, we also refer to **total margin** as **isolated margin**.


**For the crossed group**

* Total Margin = sum(Asset Balance * Reference Price * Collateral Discount Factor) for each collateral asset

Discount factor can be found in the `discountFactor` field from the [Futures Collateral Asset Info](#futures-collateral-asset-info) endpoint.


### Group Collateral Balance

**For the isolated group**

* Group Collateral Balance = isolated margin + unrealized pnl of the isolated position


**For the crossed group**

* Group Collateral Balance = total margin of the crossed group + total unrealized pnl of all positions in the crossed group


The **Group Collateral Balance** is important to determine the risk level of the margin group. If it becomes lower than the **position maintanence margin**, 
all positions in the margin group are expected to be liquidated. 


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
* Position Maintenance Margin = sum(CPN * Maintenance Margin Rate) for each contract in the crossed group



### Liquidation Price

* V = Total Margin + Unrealized Pnl - Maintenance Margin

**For long positions**

* R = abs(position size) * (1 - maintenance margin rate)
* Liquidation Price = mark price - V / R

If the calculated liquidation price is negative, the position won't be liquidation even when the price becomes zero.


**For short positions**

* R = abs(position size) * (1 + maintenance margin rate)
* Liquidation Price = mark price + V / R



### Unrealized PnL

The **Unrealized PnL** of a position is calculated as:

* Unrealized PnL = mark price * position + reference cost

Note that **position** and **reference cost** are of opposite signs.

The **Unrealized PnL** will be rolled (settled) when:

* position is closed or flipped side (long becomes short, vice versa)
* every 15 minutes AND abs(Unrealized Pnl) >= 10 USDT

Assume your current position is P, the current reference cost if RC, and unrealized PnL is L, after rolling:

* position = P
* reference cost = RC + L
* realized PnL = 0 

You should always include the unrealized PnL when calculating the collateral balance. 


### Realized PnL

**Realized Pnl** is merely a bookkeeping entry for all profits and losses realized by the current position under 
the assumption that the position was built on an average cost basis. 

If you are mostly concerned about the risk of your positions, you can ignore the realized PnL. 

