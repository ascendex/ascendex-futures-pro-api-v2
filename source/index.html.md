---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - java

toc_footers:
  - <a href='https://ascendex.com'>Sign Up for ascendex.com</a>

includes:
  - spec
  - rest
  - rest_pub_general
  - rest_pub_general_futures_products
  - rest_pub_mkt
  - rest_pub_mkt_futures_pricing_data
  - rest_prv_auth
  - rest_prv_account
  - rest_prv_account_info
  - rest_prv_account_position
  - rest_prv_free_margin
  - rest_prv_account_change_margin
  - rest_prv_account_change_margin_type
  - rest_prv_account_change_leverage
  - rest_prv_account_transfer
  - rest_prv_order
  - rest_prv_order_generate_id
  - rest_prv_order_new
  - rest_prv_order_new_batch
  - rest_prv_order_cancel
  - rest_prv_order_cancel_batch
  - rest_prv_order_cancel_all
  - rest_prv_order_open
  - rest_prv_order_hist_curr
  - rest_prv_order_query_by_id
  - wss
  - wss_general
  - wss_auth
  - wss_keep_alive
  - wss_pub
  - wss_pub_futures_pricing_data
  - wss_sub_level1
  - wss_sub_level2
  - wss_sub_trades
  - wss_sub_bar
  - wss_prv
  - wss_prv_order
  - wss_prv_account_update
  - wss_prv_req
  - wss_prv_req_account_snapshot
  - wss_prv_req_order_place
  - wss_prv_req_order_cancel
  - wss_prv_req_order_cancel_all
  - wss_prv_req_order_open
  - appendix
  - appendix_enum

header_navigators:
  - <a href="https://ascendex.github.io/ascendex-pro-api/">Cash/Margin APIs</a>
  - <a href="https://ascendex.github.io/ascendex-futures-pro-api-v2/" class="current">Futures APIs</a>

search: true

code_clipboard: true
---

# Introducing Futures Pro (v2) APIs

## Change Log

**2021-03-18**  

* Added WebSocket [*Query Open Orders*](#ws-query-open-orders) API.

**2021-03-03**

* Fixed bug of cancelling a filled order with empty fields error response.
* Added *symbol* to error response from WebSocket [*Place Order*](#ws-place-order).
* Updated *nextFundingTime* value in RESTful [*Futures Pricing Data*](#futures-pricing-data) response.
* Updated nextFundingTime *f* value in WebSocket [*Futures Pricing Data*](#channel-futures-pricing-data) message.
* Added error response demo in [*Place New Order*](#new-order).
* Added error response demo in [*Place Batch Orders*](#place-batch-orders).
* Fixed bug in [*Cancel All Open Orders*](#cancel-all-open-orders) when no data is passed in request body.
* Fixed bug of *URL Not Found* in [*Account Info*](#account-info).
* Added *openInterest* in [*Futures Pricing Data*](#futures-pricing-data)
* Added *oi* (open interest) in [*Channel: Futures Pricing Data*](#channel-futures-pricing-data)

**2021-02-26**  

* Updated *respInst* field requirement in [*Place Batch Orders*](#place-batch-orders).
* Updated *respInst* field explanation in [*Place New Order*](#new-order).

**2021-02-25**

* Updated *id* field requirement in WebSocket [*Place Order*](#ws-place-order) request.

**2021-02-23**

* Removed collapseDecimals field from [*Futures Contracts Info*](#futures-contracts-info) response.

**2021-02-22**

* Added RESTful [*Current Order History*](#list-current-history-orders) API.

**2021-02-21**

* Added [*Order Id Generate Algorithm*](#generate-order-id).
* Added RESTful [*Place Batch Orders*](#place-batch-orders) API.
* Added RESTful [*Cancel Batch Orders*](#cancel-batch-orders) API.
* Added RESTful [*Query Order By ID*](#query-order-by-id) API.

**2021-02-19**

* Added WebSocket [*Account Snapshot*](#ws-account-snapshot) API.
* Added WebSocket [*Place Order*](#ws-place-order) API.
* Added WebSocket [*Cancel Order*](#ws-cancel-order) API.
* Added WebSocket [*Cancel All Orders*](#ws-cancel-all-orders) API.

**2021-02-18**

* Replaced `baseAsset` and `quoteAsset` with `settlementAsset` in [*Futures Contract Info*](#futures-contracts-info) response.
* Updated [*Account Info*](#account-info) API path.

## Mainnet

URL: [https://ascendex.com](https://ascendex.com/)

## Testnet 

Testnet URL: [https://api-test.ascendex-sandbox.io](https://api-test.ascendex-sandbox.io/)

You are free to register one or more accounts in the testnet. You can use the magic code **888888** to bypass all verification code checks 
(email verification, phone number verification, two-step authentication, etc.).

You accounts will automatically receive initial funding. 

Please expect the testnet to be reset every a few days. 

## Obtain API Keys

Prior to use API, you need to login the website to create API Key with proper permissions. The API key is shared for all instruments in AscendEx including cash, margin and futures.

You can create and manage your API Keys [here](https://ascendex.com/en/account/api-key).

Every user can create up to 10 API Keys, each can be applied with either permission below:

- **View permission**: It is used to query the data, such as order query, trade query.
- **Trade permission**: It is used to place order, cancel order and transfer, etc.
- **Transfer permission**: It is used to create/cancel asset transfer order, etc.

Please remember below information after creation:

- **Access Key** is used in API request
- **Secret Key** is used to generate the signature (only visible once after creation)
- The API Key can bind maximum 20 IP addresses (either host IP or network IP), we strongly suggest you bind IP address for security purpose. The API Key without IP binding will be expired after 90 days.



## SDKs and Client Libraries

### Official SDK

**CCXT** is our authorized SDK provider and you may access the AscendEX API through CCXT. For more information, please visit: https://ccxt.trade.

### Demo Code

Python Demo: [https://github.com/ascendex/ascendex-futures-api-demo-v2](https://github.com/ascendex/ascendex-futures-api-demo-v2)


## Market Making Incentive Program

AscendEX offers a Market Making Incentive Program for professional liquidity providers. Key benefits of this program include:

* Favorable fee structure.
* Monthly bonus pending satisfying KPI.
* Direct Market Access and Co-location service.

Users with good maker strategies and significant trading volume are welcome to participate in this long-term program. If your account has a trading volume of more than 150,000,000 USDT in the last 30 days on any exchange, please send the following information via email to institution@ascendex.com, with the subject "Market Maker Incentive Application":

* One AscendEX account ID.
* A brief explanation of your market making method (NO detail is needed), as well as estimation of maker orders' percentage.

