---
title: title

language_tabs: # must be one of https://git.io/vQNgJ


toc_footers:
  - <a href='https://www.kucoin.com'>Sign Up for KuCoin</a>

includes:

search: true
---

# General

## Introduction 

Welcome to KuCoin’s trader and developer documentation. These documents outline the exchange functionality, market details, and APIs.

The whole documentation is divided into two parts: REST API and Websocket feed.

The REST API contains four sections: User(private) , Trade(private), Market Data(public) and Others(public).

The WebSocket contains two sections: Public Channels and Private Channels

## Upcoming Changes

To get the latest updates in API, you can click ‘Watch’ on our [KuCoin Docs Github](https://github.com/Kucoin/kucoin-api-docs).

**10/17/19**: 

- Add the **remark** field to [Get Deposit List](#get-deposit-list) and [Get Withdrawals List](#get-withdrawals-list)

**10/12/19**: 

- Merge [Get Market List](get-market-list) ETH、NEO、TRX three markets into ALTS.

**9/27/19**

- Add **symbolName** response to [Get All Tickers](#get-all-tickers).

**10/09/19**: 

- Deprecate '/api/v1/accounts/inner-transfer' endpoint for [Inner Transfer](#inner-transfer).
- Add the **margin** type for [List Accounts](#list-accounts). 
- Support the margin account for [Get an Account](#get-an-account).
- Add the **margin** type for [Create an Account](#create-an-account).
- Add the extra bizType for margin via [Get Account Ledgers](#get-account-ledgers).
- Add the extra bizType for margin via [Get Holds](#get-holds) 
- Add the margin account via [Get Account Balance of a Sub-Account](#get-account-balance-of-a-sub-account)
- Support the margin account for [Get the Aggregated Balance of all Sub-Accounts](#get-the-aggregated-balance-of-all-sub-accounts)
- Add the **MARGIN** type for [Transfer between Master user and Sub-user](#transfer-between-master-user-and-sub-user) 
- Add the **margin** type for [Inner Transfer](#inner-transfer) 
- Add [Get the Transferable Balance].

**6/19/19**: 

- Modify [Transfer between Master user and Sub-user](#transfer-between-master-user-and-sub-user)

**6/13/19**: 

- Add [FAQ](#faq) for Open API.
- Add the advantage descriptions for [Level-3](#matchengine-data).

**5/28/19**: 

- Modify [Get Market List](#Get-Market-List) SC changed to USDS.
- Add one new endpoint for [Inner Transfer](#inner-transfer), the original interface will expire after three months (8/28/19).
- Add the usage description to the favorite withdrawal address [Apply Withdraw](#apply-withdraw).
- Add **averagePrice** field to [Get 24hr Stats](#get-24hr-stats).
  
**5/8/19** : 

- Add **chain** field to [Create Deposit Address](#create-deposit-address), [Get Deposit Address](#get-deposit-address), [Get Currency Detail](#get-currency-detail), [Get Withdrawal Quotas](#get-withdrawal-quotas) and [Apply Withdraw](#apply-withdraw).
-  Add the description of how to transfer assets in the [Inner Transfer](#inner-transfer) interface. 
- Add **L3 demo** to [Full MatchEngine Data(Level 3)](#full-matchengine-data(level-3)).
- modify the strategy of [Rate Limit](#request-rate-limit).

**4/24/19**: 

- Delete the "size" and "funds" fields of the “received” message in the subscription for [Full MatchEngine Data(Level 3)](#full-matchengine-data(level-3)) via the public channels, therefore protecting the hidden orders. These fields in the private channels remain unchangeds.
- Delete the “remainSize” field of the “open” messages in the subscription for [Full MatchEngine Data(Level 3)](#full-matchengine-data(level-3)) via the public channels, therefore protecting the hidden orders. These fileds in the private channels remain unchanged.
- Add [Get User Info of all Sub-Accounts](#get-user-info-of-all-sub-accounts).
- Add [Get Account Balance of a Sub-Account](#get-account-balance-of-a-sub-account).
- Add [Get the Aggregated Balance of all Sub-Accounts of the Current User](#get-the-aggregated-balance-of-all-sub-accounts-of-the-current-user).
- Add [Transfer between Master account and Sub-Account](#transfer-between-master-account-and-sub-account).

**3/27/19** : 

- Add **feeCurrency** field to [Get Symbols List](#get-symbols-list).

**3/25/19** : 

- Add **volValue** field to [Get All Tickers](#get-all-tickers).
- Add **clientOid** field to [Full MatchEngine Data(Level 3)](#full-matchengine-data(level-3))which allows you to filter your order info by clientOid when you subscribe to the "received " messages through private channels.
- Add **accountId** field in the subscription for [Account balance notice](#account-balance-notice).

**3/13/19** : 

- Modify the maximum matching orders for a single trading pair in one account is 200 (stop orders included).

**3/6/19** : 

- Add **nanoseconds** as the time unit of the order system and matching engine.

**2/28/19** : 

- Modify [Get Symbols List](#get-symbols-list) response description
- Add [Get V1 Historical Deposits List](#get-v1-historical-deposits-list)
- Add [Get V1 Historical Withdrawals List](#get-v1-historical-withdrawals-list)
- Add [Get V1 Historical Orders List](#get-v1-historical-orders-list)
- Add explanation to part of the API JSON field
- Delete "sn" field in [Match Execution Data](#match-execution-data) 
- Modify [Get Fiat Price](#get-fiat-price) parameter description
- Add "acceptUsermessage" option when connecting to the WebSocket.

**2/22/19** : 

- Add **volValue** field to [Get 24hr Stats](#get-24hr-stats)

**2/21/19** : 

- Add [Get Full Order Book(aggregated) v2](#get-full-order-book-aggregated) 
- Add **time** field to Level-1,2,3 Data 
- Add [Get Fiat Price](#get-fiat-price)

**2/20/19** : 

- Add **time** field to [Get All Tickers](#get-all-tickers) and [Get Ticker](#get-ticker) 

**2/19/19** : 

- Add [Get All Tickers](#get-all-tickers)

**2/18/19** : 

- Add [Recent Orders](#recent-orders)
- Add [Recent Fills](#recent-fills)

**2/16/19** : 

- Add [All Symbols Ticker](#all-symbols-ticker)
- Modify [Permissions](#permissions)

**1/30/19** : 

- Add SDK official provider [CCXT](#client-libraries)

**1/25/19** : 

- Add [Get Market List](#get-market-list)
- Add [Symbol Snapshot Feed](#symbol-snapshot)
- Add [Market Snapshot Feed](#market-snapshot)
- Add official [Java & Go SDK](#client-libraries)
  
## Reading Guide

1. Read [Sandbox](#sandbox) to learn how to debug API in a test environment.
2. Read [REST API](#rest-api) to learn how to build a request.
3. Read [Time](#time) if you want to make a test request (and receive a sample response) without having to authorize.
4. Read [Authentication](#authentication) to learn how to make an authorized request.
5. Read [Inner Transfer](#inner-transfer) to see how to transfer assets.
6. Read [List Accounts](#list-accounts) to learn how to get the data of your account balance.
7. Read [Place a new order](/#place-a-new-order) to see how to place an order.
8. Read [Order Book](#get-part-order-book-aggregated) to get a snapshot of the order book.
9. Read [Websocket Feed](#websocket-feed) to learn how to establish a websocket connection.
10. Read [Level-2 Market Data](#level-2-market-data) to see how to build a local real-time order book with websocket. 
11. Read [Account balance notice](#account-balance-notice) to see how to get a private websocket feed and get real time notice of balance changes.
    
## Sub-account

You can create a sub-account and its API key on the web end.

A sub-account can be used to separate the funds for crypto tradings and the funds can be transferred between the master account and the sub-account. Please note that the funds in sub-account is limited for sub-account crypto trading only and the funds cannot be withdrawn directly from the sub-account.

The API of a sub-account is available to access all the public endpoints. Besides this, traders can access the following private endpoints via the API key of a sub-account: 


Endpoints | Description
---------- | -------
[List Accounts](#list-accounts) | Get the status of an account.
[Get an Account](#get-an-account) | Get the info of an account.
[Create an Account](#create-an-account) | Create an Account.
[Get Account Ledgers](#get-account-ledgers) | Get the funds details of an account.
[Get Holds](#get-holds) | Get the hold details of an account.
[Inner Transfer](#inner-transfer) | Transferring assets between the accounts of main and trade.
[Place a new order](#place-a-new-order) | Place an order.
[Cancel an order](#cancel-an-order) | Request to cancel an order.
[Cancel all orders](#cancel-all-orders) | Request to cancel all orders.
[List Orders](#list-orders) | Get orders details.
[Recent Orders](#recent-orders) | Get order details of the last 24 hours(up to 1000).
[Get an order](#get-an-order) | Get the details of a single order.
[List Fills](#list-fills) | Get the order execution details.
[Recent Fills](#recent-fills) | Get order execution details of the last 24 hours(up to 1000).

 A sub-account shares the same fee level as its master-account. (The fee level will be calculated based on the total transaction amount of the sub-account and the master account or the holding amount of KCS.)

The sub-account needs to transfer funds from the main account to the trade account before trading.

<aside class="notice">The withdrawal and deposit is not supported for sub-account.</aside>


## Matching Engine

### Order Lifecycle

Valid orders sent to the matching engine are confirmed immediately and are in the **received** state. If an order executes against another order immediately, the order is considered **done**. An order can execute in part or whole. Any part of the order not filled immediately, will be considered **open**. Orders will stay in the open state until canceled or subsequently filled by new orders. Orders that are no longer eligible for matching (filled or canceled) are in the **done** state.

### Self-Trade Prevention

**Self-Trade Prevention** is an option in advanced settings.It is not selected by default. If you specify STP when placing orders, your order won't be matched by another one which is also yours. On the contrary, if STP is not specified in advanced, your order can be matched by another one of your own orders.


#### DECREMENT AND CANCEL(DC)

**Market orders are currently not supported for DC**. When two orders from the same user cross, the smaller order will be canceled and the larger order will be decremented by the size of the smaller order. If the two orders are the same size, both will be canceled.

#### CANCEL OLDEST(CO)

Cancel the older (resting) order in full. The new order continues to execute.

#### CANCEL NEWEST(CN)

Cancel the newer (taking) order in full. The old resting order remains on the order book.

#### CANCEL BOTH(CB)

Immediately cancel both orders.

### MatchEngine Data

#### Level-3 Market Data（Recommend）

The data pushed by the matching engine is the information of each order, which is the market data of Level-3.<br/>
The Level-3 market data is more suitable for high-frequency traders.<br/>

You can subscribe [Level-3 Market Data] (#full-matchengine-data-level-3) via WebSocket:

* Get real-time market information in the market faster (push speed: Level-3 >= Level-2)
* Can be used to build and maintain order book
* Can get the reason for the quantity change of a single order
* Get real-time access to orders 
* Can completely replace most of the pull API function of the Rest API (There is a strict rate limit on Rest request)
  
For the processing of different types of information, please refer to [Level-3 demo] (#client-libraries) or [Message Type] (#full-matchengine-data-level-3) of Level-3 below.



## Client Libraries

Client libraries can help you integrate with our API quickly.

**Official SDK of KuCoin**

- [Java SDK](https://github.com/Kucoin/KuCoin-Java-SDK)
- [PHP SDK](https://github.com/Kucoin/KuCoin-PHP-SDK)
- [Go SDK](https://github.com/Kucoin/KuCoin-Go-SDK)
- [Level3-Demo](https://github.com/Kucoin/kucoin-go-level3-demo)


CCXT is our authorized SDK provider and you may access the KuCoin API through CCXT. For more information, please visit: [https://ccxt.trade](https://ccxt.trade).

**Unofficial SDK of KuCoin**

Thanks to the great community contributors, these are the open-source SDKs contributed by community developers. Since each library is updated frequently, KuCoin does not review all source code and does not rigorously test it. KuCoin is not responsible for the security of the SDK. Please conduct a basic code review and assess the risks before use
and we recommend you to check the **pull requests** and **issues** before the usage.

- Python [sammchardy/python-kucoin](https://github.com/sammchardy/python-kucoin)
- .NET [mscheetz/KuCoinApi.Net](https://github.com/mscheetz/KuCoinApi.Net/tree/v2.0)

If you are a developer, [submit](https://github.com/Kucoin) your SDK to us and get KCS rewards.

**Examples**

- PHP File Example (GET & POST & DELETE)  [Github Link](https://github.com/Kucoin/kucoin-api-docs/tree/master/examples/php)

- - -

## Sandbox


**Sandbox is the test environment**, used for testing an API connection or web trading. It provides all the functionalities of the live exchange. All funds and transactions there are simulated for testing purposes.

The login session and the API key in the sandbox environment are completely separated from the production environment. You may use the web interface in the sandbox environment to create an API key.

Notice: After registering in the sandbox environment, you will receive a nummber amount of fake funds (BTC, ETH or KCS) automatically released by the system in your account. If you want to **trade**, please transfer assets from the  **main**  account to the  **trade** account. The funds are only for test purposes and cannot be withdrawn.


Sandbox URLs for API test:

Website:
**[https://sandbox.kucoin.com](https://sandbox.kucoin.com)**

REST API:
**https://openapi-sandbox.kucoin.com**


## Request Rate Limit

When a rate limit is exceeded, a status of **429 Too Many Requests** will be returned.
If the rate limit is exceeded multiple times, the system will restrict your use of your IP and account for at least 1 minute. Your remaining request times will be returned in the results.

###REST API

The access limit for REST API is applied per API key. For average users, the request limit for each API key is **1800 requests per minute**. The limit strategy is applicable for both public and private endpoints 

####Hard-Limits

[List Fills](#list-fills): 100 requests per 10 seconds(will be restricted for 10 seconds if the limit is exceeded)

[List orders](#list-orders): 200 requests per 10 seconds(will be restricted for 10 seconds if the limit is exceeded)


###WEBSOCKET


### Number of Connections
Number of connections per user ID:   ≤ 10

### Connection Times
Connection Limit: 30 per minute


### Number of Uplink Messages 
Message limit sent to the server: 100 per 10 seconds

 
### Topic Subscription Limit
Subscription limit for each connection: 100 topics



### Apply for Higher Request Rate Limit
If you are a professional trader or market maker and need a higher limit, please send your KuCoin account, reason and approximate trading volume to [api@kucoin.com](mailto:api@kucoin.com).


## Market Making Incentive Scheme

KuCoin offers a Market Making Incentive Scheme for professional liquidity providers. Key benefits of this program include:

- Market Maker rebate.
- Monthly rewards up to 30,000 KCS for the market maker with the best performance.
- Direct Market Access and Co-location service.

Users with good maker strategies and huge trading volume are welcome to participate in this long-term program. If your account has a trading volume of more than 5000 BTC in the last 30 days on any exchange, please send the following information via email to **mm@kucoin.com**, with subject "Spot Market Maker Application":

- One KuCoin account ID (a non-referred account is required).
- Proof of volume traded on any exchange within the past 30 days. Proof of a VIP level is also acceptable.
- A brief explanation of your market making method (NO detail is needed), as well as estimation of maker orders’ percentage.

## VIP Fast Track

KuCoin now provides a VIP fast track to users with a large trading volume in crypto. If your accounts on different platforms have a total trading volume of more than 1000 BTC in the last 30 days, please send the following information via email to **vip@kucoin.com**, with subject "VIP Fast Track Application":

KuCoin account ID.
Proof of trading volume on other platforms within the past 30 days. Proof of a VIP level is also acceptable.

We will offer you a jumpstart (e.g. a VIP level which matches your volume on other exchanges even though you are not trading as much on KuCoin) for 30 days. After 30 days, your VIP level will be calculated based on your actual trading volume on KuCoin.

For more information on the VIP fee, you can read: [Tiered Trading Fee Discount Program](https://www.kucoin.com/news/en-fee).



## FAQ

### Invalid Signature


* Check if your API-KEY, API-SECRET and API-PASSPHRASE are correct
* Check if the string sequence is correct: timestamp + method + requestEndpoint + body
* Check whether the timestamp in header is the same with the content above
* Check whether you are using the correct encoding in your signature, e.g. base64
* Check whether the **GET** request is submitted as a form
* Check whether the content-type of your POST request is in application/json form and is encoded by charset=utf-8
  
### Apply Withdraw
* memo
  
For currencies without memo, the memo field is not required. Please do not pass the parameter when you are applying to withdraw via API, or the system will return: **kucoin incorrect withdrawal address**.<br/>

* amount
  
The precision of the **amount** field shall satisfy the withdrawal precision requirements of the currency. The precision requirements for the currencies can be obtained by [Withdrawals Quotas](#get-withdrawal-quotas).
The withdrawal amount must be an integer multiple of the withdrawal accuracy. If the withdrawal accuracy is 0, the withdrawal amount it can only be an integer.


### .net SDK 
* Invalid Signature on POST Request

"{\"code\":\"400005\",\"msg\":\"Invalid KC-API-SIGN\"}"<br/>
There is a bug in the code:<br/>
 var response = body == null ? await _restRepo.PostApi<ApiResponse<T>, SortedDictionary<string, object>>(url, body, headers) : await _restRepo.PostApi<ApiResponse<T>>(url, headers);<br/>
After fixing:<br/>
 var response = body != null ? await _restRepo.PostApi<ApiResponse<T>, SortedDictionary<string, object>>(url, body, headers) : await _restRepo.PostApi<ApiResponse<T>>(url, headers);

### WebSocket
* Subscription limit for each connection: 100 topics;
* Validity period for token: 24 hours;
* Number of connections per user: ≤ 10
* Number of Messages of the client side: 100 per 10 seconds;
* Subscribing one symbol means subscribing a topic; (e.g.Topic: /market/level3:{symbol},{symbol}...) 

### 403  Error

If an error occurs as follows:
403 "The request could not be satisfied. Bad Request" from Amazon CloudFront<br/>

* Check whether the request is HTTPS
* Remove the RequestBody from the GET request





# REST API

## Base URL

The REST API has endpoints for account and order management as well as public market data.

The base url is **https://api.kucoin.com**.  

The request URL needs to be determined by BASE and specific endpoint combination. 

## Endpoint of the Interface


Each interface has its own endpoint, described by field **HTTP REQUEST** in the docs. 

For the **GET METHOD** API, the endpoint needs to contain the query parameters string.

E.G. For "List Accounts", the default endpoint of this API is **/api/v1/accounts**. If you pass the "currency" parameter(BTC), the endpoint will become **/api/v1/accounts?currency=BTC** and the final request URL will be **https://openapi-v2.kucoin.com/api/v1/accounts?currency=BTC**.


## Request
All requests and responses are **application/json** content type.  

Unless otherwise stated, all timestamp parameters should in milliseconds. e.g. **1544657947759**

### Parameters

For the **GET, DELETE** request, all query parameters need to be included in the request url. (**e.g. /api/v1/accounts?currency=BTC**)

For the **POST, PUT** request, all query parameters need to be included in the request body with JSON. (**e.g. {"currency":"BTC"}**). **Do not include extra spaces in JSON strings.**

### Errors

When errors occur, the HTTP error code or system error code will be returned. The body will also contain a message parameter indicating the cause.

#### HTTP error status codes

```
{
  "code": "400100",
  "msg": "Invalid Parameter."
}

```

Code | Meaning
---------- | -------
400 | Bad Request -- Invalid request format.
401 | Unauthorized -- Invalid API Key.
403 | Forbidden -- The request is forbidden.
404 | Not Found -- The specified resource could not be found.
405 | Method Not Allowed -- You tried to access the resource with an invalid method.
415 | Unsupported Media Type. You need to use: application/json.
429 | Too Many Requests -- Access limit breached.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.


#### System error codes

Code | Meaning
---------- | -------
400001 | Any of KC-API-KEY, KC-API-SIGN, KC-API-TIMESTAMP, KC-API-PASSPHRASE is missing in your request header
400002 | KC-API-TIMESTAMP Invalid -- Your time differs from the server time by more than 5 seconds
400003 | KC-API-KEY doesn’t exist
400004 | KC-API-PASSPHRASE error
400005 | Signature error -- Please check your signature
400006 | The requested IP address is not in the API whitelist
400007 | Access Denied -- Your API-key does not have sufficient permissions to access the URL
404000 | Url Not Found -- The requested resource could not be found
400100 | Parameter Error -- You tried to access the resource with invalid parameters
411100 | User is frozen -- The user is frozen, please contact us via support center.
500000 | Internal Server Error -- We had a problem with our server. Try again later.

If the returned HTTP status code is 200, whereas the operation failed, an error will occur. You can check the above error code for details.

### Success

A successful response is indicated by an HTTP status code 200 and system code 200000. The success response is as follows: 


```
{
  "code": "200000",
  "data": "1544657947759"
}
```



### Pagination

Pagination allows for fetching results with the current page and is well suited for real time data. Endpoints like /api/v1/deposits, /api/v1/orders, /api/v1/fills, will return the latest items by default (50 pages in total). To retrieve more results, users should specify the currentPage number in the subsequent requests to turn the page based on the data previously returned.

#### PARAMETERS 

Parameter | Default | Description
---------- | ------- | ------
currentPage | 1 | Current request page.
pageSize | 50 | Number of results per request.


### Example
**GET /api/v1/orders?currentPage=1&pageSize=50**


## Types 

### Timestamps 

Unless otherwise specified, all timestamps from API are returned in **milliseconds**(e.g. **1546658861000**). Most modern languages and libraries will handle this without issues. 

But please note that the timestamps between the **matching engine** and the **order** system are in nanoseconds.

### Numbers 
Decimal numbers are returned as strings in order to preserve the full precision across platforms. When making a request, it is recommended that you also convert your numbers to strings to avoid truncation and precision errors.

## Authentication

### Generating an API Key

Before being able to sign any requests, you must create an API key via the KuCoin website. Upon creating a key you need to write down 3 pieces of information:


* Key
* Secret
* Passphrase

The Key and Secret are generated and provided by KuCoin and the Passphrase refers to the one you used to create the KuCoin API. Please note that these three pieces of information can not be recovered once lost. If you lost this information, please create a new API KEY.

### Permissions

You can manage the API permission on KuCoin’s official website. The permissions are:


* **General** - General - Allows a key general permissions. This includes most of the GET endpoints.
* **Trade** -  Allows a key to create orders and inner transfer funds.
* **Transfer** -  Allows a key to transfer funds (including deposit and withdrawal). Please note a sub-account is not authorized this permission. Enable with caution - API key transfers WILL BYPASS two-factor authentication.


Please refer to the documentation below to see what API key permissions are required for a specific route.

### Creating a Request

All private REST requests must contain the following headers:

* **KC-API-KEY** The API key as a string.
* **KC-API-SIGN** The base64-encoded signature (see Signing a Message).
* **KC-API-TIMESTAMP** A timestamp for your request.
* **KC-API-PASSPHRASE** The passphrase you specified when creating the API key.

### Signing a Message

```php
    <?php
    class API {
        public function __construct($key, $secret, $passphrase) {
          $this->key = $key;
          $this->secret = $secret;
          $this->passphrase = $passphrase;
        }

        public function signature($request_path = '', $body = '', $timestamp = false, $method = 'GET') {
          
          $body = is_array($body) ? json_encode($body) : $body; // Body must be in json format
          
          $timestamp = $timestamp ? $timestamp : time() * 1000;

          $what = $timestamp . $method . $request_path . $body;

          return base64_encode(hash_hmac("sha256", $what, $this->secret, true));
        }
    }
    ?> 
```

```python
    #Example for get balance of accounts in python
    
    api_key = "api_key"
    api_secret = "api_secret"
    api_passphrase = "api_passphrase"
    url = 'https://openapi-sandbox.kucoin.com/api/v1/accounts'
    now = int(time.time() * 1000)
    str_to_sign = str(now) + 'GET' + '/api/v1/accounts'
    signature = base64.b64encode(
        hmac.new(api_secret.encode('utf-8'), str_to_sign.encode('utf-8'), hashlib.sha256).digest())
    headers = {
        "KC-API-SIGN": signature,
        "KC-API-TIMESTAMP": str(now),
        "KC-API-KEY": api_key,
        "KC-API-PASSPHRASE": api_passphrase
    }
    response = requests.request('get', url, headers=headers)
    print(response.status_code)
    print(response.json())
    
    #Example for create deposit addresses in python
    url = 'https://openapi-sandbox.kucoin.com/api/v1/deposit-addresses'
    now = int(time.time() * 1000)
    data = {"currency": "BTC"}
    data_json = json.dumps(data)
    str_to_sign = str(now) + 'POST' + '/api/v1/deposit-addresses' + data_json
    signature = base64.b64encode(
        hmac.new(api_secret.encode('utf-8'), str_to_sign.encode('utf-8'), hashlib.sha256).digest())
    headers = {
        "KC-API-SIGN": signature,
        "KC-API-TIMESTAMP": str(now),
        "KC-API-KEY": api_key,
        "KC-API-PASSPHRASE": api_passphrase,
        "Content-Type": "application/json" # specifying content type or using json=data in request
    }
    response = requests.request('post', url, headers=headers, data=data_json)
    print(response.status_code)
    print(response.json())
```

For the header of KC-API-KEY, 
* Use API-Secret to encrypt the prehash string {timestamp+method+endpoint+body } with sha256 HMAC. The request body is a JSON string and need to be the same with the parameters passed by the API.
* After that, use base64-encode to encrypt the result in step 1 again.

Notice: 

* The encrypted timestamp shall be consistent with the KC-API-TIMESTAMP field in the request header. 
* The body to be encrypted shall be consistent with the content of the Request Body.  
* The Method should be UPPER CASE.
* For GET, DELETE request, the endpoint needs to contain the query string. e.g. /api/v1/deposit-addresses?currency=XBT. The body is "" if there is no request body (typically for GET requests).



```python
#Example for Create Deposit Address

curl -H "Content-Type:application/json" -H "KC-API-KEY:5c2db93503aa674c74a31734" -H "KC-API-TIMESTAMP:1547015186532" -H "KC-API-PASSPHRASE:Abc123456" -H "KC-API-SIGN:7QP/oM0ykidMdrfNEUmng8eZjg/ZvPafjIqmxiVfYu4=" 
-X POST -d '{"currency":"BTC"}' http://openapi-v2.kucoin.com/api/v1/deposit-addresses

KC-API-KEY = 5c2db93503aa674c74a31734
KC-API-SECRET = f03a5284-5c39-4aaa-9b20-dea10bdcf8e3
KC-API-PASSPHRASE = Abc123456
TIMESTAMP = 1547015186532
METHOD = POST
ENDPOINT = /api/v1/deposit-addresses
STRING-TO-SIGN = 1547015186532POST/api/v1/deposit-addresses{"currency":"BTC"}
KC-API-SIGN = 7QP/oM0ykidMdrfNEUmng8eZjg/ZvPafjIqmxiVfYu4=
```

<aside class="spacer16"></aside>
<aside class="spacer8"></aside>

### Selecting a Timestamp

The **KC-API-TIMESTAMP** header MUST be number of **milliseconds** since Unix Epoch in UTC. e.g. 1547015186532

Decimal values are allowed, e.g. 1547015186532. But you need to be aware that timestamp between match and order is **nanosecond**.

The difference between your timestamp and the API service time must be less than **5 seconds** , or your request will be considered expired and rejected. We recommend using the time endpoint to query for the API [server time](/#time) if you believe there may be time skew between your server and the API server.



  
# User
Signature is required for this part.


# User Info

## Get User Info of all Sub-Accounts

```json
[{
		"userId": "5cbd31ab9c93e9280cd36a0a",  //subUserId
		"subName": "kucoin1",
		"remarks": "kucoin1"
	},
	{
		"userId": "5cbd31b89c93e9280cd36a0d",
		"subName": "kucoin2",
		"remarks": "kucoin2"
	}
]
```

You can get the user info of all sub-users via this interface.

### HTTP REQUEST

**Get /api/v1/sub/user**


### Example
GET /api/v1/sub/user

### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.

### RESPONSES

Field | Description
--------- | ------- 
userId | The user ID of your sub-account
subName | The username of your sub-account
remarks | Remark



# Account

## Create an Account
```json
{
    "id": "5bd6e9286d99522a52e458de"  //accountId
}
```

### HTTP REQUEST
**POST /api/v1/accounts**

### Example
POST /api/v1/accounts


### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.

### Parameters

Param | Type | Description
--------- | ------- | ------- 
type | String | Account type: **main**, **trade**, **margin**
currency | String | [Currency](#get-currencies) 

### RESPONSES
Field | Description
--------- | ------- 
id | accountId, ID of an account


## List Accounts

```json
[{
    "id": "5bd6e9286d99522a52e458de",  //accountId
    "currency": "BTC",  //Currency
    "type": "main",     //Account type, including main and trade
    "balance": "237582.04299",  //Total assets of a currency
    "available": "237582.032",  //Available assets of a currency
    "holds": "0.01099". //Hold assets of a currency
},
{
    "id": "5bd6e9216d99522a52e458d6",
    "currency": "BTC",
    "type": "trade",
    "balance": "1234356",
    "available": "1234356",
    "holds": "0"
}]

```
Get a list of accounts.

Please deposit funds to the main account firstly, then transfer the funds to the trade account via [Inner Transfer](#inner-transfer) before transaction.

### HTTP REQUEST
**GET /api/v1/accounts**

### Example
GET /api/v1/accounts

### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.

### Parameters

Param | Type | Description
--------- | ------- | ------- 
currency | String | *[Optional]* [Currency](#get-currencies) 
type | String | *[Optional]* Account type: **main**, **trade** or **margin**  

### RESPONSES
Field | Description
--------- | ------- 
id | The ID of the account 
currency | Currency
type | Account type: **main**, **trade** or **margin**
balance | Total funds in the account 
available | Funds available to withdraw or trade 
holds | Funds on hold (not available for use) 

### ACCOUNT TYPE
There are three types of accounts: 1) **main** account 2) **trade** account 3) **margin** account. 

No fees will be charged for the funds transfer between these account.

The main account is used for the storage, withdrawal, and deposit of the funds. The assets in the main account cannot be directly used for trading. To trade cryptos, you need to transfer funds from the main account to the trade account.

The trading account is used for transaction. When you place an order, the system will use the balance of the  trade account. You can’t withdraw funds directly from a trade account. To withdraw the funds, you need to transfer the funds from the trade account to the main account firstly.

The margin account is used to borrow assets and leverage transactions.

### FUNDS ON HOLD
When placing an order, the funds for the order will be freezed. The freezed funds cannot be used for other order placement or withdrawal and will remain on hold until the order is filled or cancelled.



## Get an Account
```json
{
    "currency": "KCS",  //Currency
    "balance": "1000000060.6299",  //Total assets of a currency
    "available": "1000000060.6299",  //Available assets of a currency
    "holds": "0". //Hold assets of a currency
}
```
Information for a single account. Use this endpoint when you know the accountId.

### HTTP REQUEST
**GET /api/v1/accounts/{accountId}**

### Example
GET /api/v1/accounts/5bd6e9286d99522a52e458de

### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.


### Parameters

Param | Type | Description
--------- | ------- | ---------
accountId | String | **Path parameter.** ID of the account

### RESPONSES
Field | Description
--------- | ------- 
currency | The currency of the account 
balance | Total funds in the account 
holds | Funds on hold (not available for use) 
available | Funds available to withdraw or trade 



## Get Account Ledgers 

Request via this endpoint to get the account ledgers.

Items are paginated and sorted to show the latest first. See the [Pagination](#pagination) section for retrieving additional entries after the first page.


```json
{
	"currentPage": 1,
	"pageSize": 10,
	"totalNum": 3,
	"totalPage": 1,
	"items": [{
			"currency": "KCS",  //Currency
			"amount": "0.0998", //Change amount of the funds
			"fee": "0",  //Deposit or withdrawal fee
			"balance": "1994.040596",  //Total assets of a currency
			"bizType": "Withdraw",  //business type
			"direction": "in",     //side, in or out 
			"createdAt": 1540296039000,  //Creation time
			"context": {          //Business core parameters
				"orderId": "5bc7f080b39c5c03286eef8a",
				"txId": "bf848bfb6736780b930e12c68721ea57f8b0484a4af3f30db75c93ecf16905c9"
			}
		},
		{
			"currency": "KCS",
			"amount": "0.0998",
			"fee": "0",
			"balance": "1994.140396",
			"bizType": "Deposit",
			"direction": "in",
			"createdAt": 1540296039000,
			"context": {
				"orderId": "5bc7f080b39c5c03286eef8a",
				"txId": "bf848bfb6736780b930e12c68721ea57f8b0484a4af3f30db75c93ecf16905c9"
			}
		},
		{
			"currency": "KCS",
			"amount": "0.0998",
			"fee": "0",
			"balance": "1994.140396",
			"bizType": "trade exchange",
			"direction": "in",
			"createdAt": 1540296039000,
			"context": {
				"orderId": "5bc7f080b39c5c03286eef8e",
				"tradeId": "5bc7f080b3949c03286eef8a",
				"symbol": "BTC-USD"
			}
		}
	]
}
```

### HTTP REQUEST
**GET /api/v1/accounts/{accountId}/ledgers**

### Example
GET /api/v1/accounts/5bd6e9286d99522a52e458de/ledgers


### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.

<aside class="notice">This request is paginated.</aside>

### Parameters

Param | Type | Description
--------- | ------- | ------- 
accountId | String | ID of the account 
startAt| long | *[Optional]*  Start time (milisecond)
endAt| long | *[Optional]* End time (milisecond)

### RESPONSES
Field | Description
--------- | ------- 
currency | The currency of an account 
amount | The total amount of assets (fees included) involved in assets changes such as transaction, withdrawal and bonus distribution. 
fee | Fees generated in transaction, withdrawal, etc.
balance | Remaining funds after the transaction.
bizType | Business type leading to the changes in funds, such as exchange, withdrawal, deposit,  KUCOIN_BONUS, REFERRAL_BONUS, Lendings etc. 
direction | Side, **out** or **in**
createdAt | Time of the event
context | Business related information such as order ID, serial No., etc.

### context
If the returned value under bizType is **“trade exchange”**, the additional info. (such as order ID and trade ID, trading pair, etc.) of the trade will be returned in field **context**. 



## Get Holds 

```json
{
    "currentPage": 1,
    "pageSize": 10,
    "totalNum": 2,
    "totalPage": 1,
    "items": [
        {
            "currency": "ETH",  //Currency
            "holdAmount": "5083",  //Hold amount of a currency
            "bizType": "Withdraw",     //business type
            "orderId": "5bc7f080b39c5c03286eef8e", // ID of funds freezed order 
            "createdAt": 1545898567000, //Creation time
            "updatedAt": 1545898567000。//update time
        },
        {
            "currency": "ETH",
            "holdAmount": "1452",
            "bizType": "Withdraw",
            "orderId": "5bc7f518b39c5c033818d62d",
            "createdAt": 1545898567000,
            "updatedAt": 1545898567000
        }
    ]
}
```

Holds are placed on an account for any active orders or pending withdraw requests. As an order is filled, the hold amount is updated. If an order is canceled, any remaining hold is removed. For a withdraw, once it is completed, the hold is removed.

### HTTP REQUEST
**GET /api/v1/accounts/{accountId}/holds**

### Example
GET /api/v1/accounts/5bd6e9286d99522a52e458de/holds

### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.

<aside class="notice">This request is paginated.</aside>

### Parameters

Param | Type | Description
--------- | ------- | ------- 
accountId | String | ID of the account. 



### RESPONSES
Field | Description
--------- | -------
currency | currency
holdAmount | Remaining funds frozen (calculated by subtracting any unfrozen funds from the initial frozen funds))
bizType | Business type which led to the freezing of the funds, such as transaction, withdrawal, lendings etc.
orderId | ID of funds freezed order (this ID is unique to the frozen asset order) 
createdAt | Time of the event
updatedAt | Update time


### bizType
The **bizType** field indicates the reason for the account hold.

###orderId
The **orderId** field is a unique order ID generated in order placement or withdrawal.



## Get Account Balance of a Sub-Account

```json
{
	"subUserId": "5caefba7d9575a0688f83c45", 
	"subName": "sdfgsdfgsfd",
	"mainAccounts": [{
		"currency": "BTC",
		"balance": "8",
		"available": "8",
    "holds": "0",
    "baseCurrency": "BTC",
    "baseCurrencyPrice": "1",
    "baseAmount": "1.1"
	}],
	"tradeAccounts": [{
		"currency": "BTC",
		"balance": "1000",
		"available": "1000",
    "holds": "0",
    "baseCurrency": "BTC",
    "baseCurrencyPrice": "1",
    "baseAmount": "1.1"

  }],
  "marginAccounts": [{
    "currency": "BTC",
    "balance": "1.1",
    "available": "1.1",
    "holds": "0",
    "baseCurrency": "BTC",
    "baseCurrencyPrice": "1",
    "baseAmount": "1.1"
  }]
}
```

This endpoint returns the account info of a sub-user specified by the subUserId.

###HTTP REQUEST

**GET /api/v1/sub-accounts/{subUserId}**

### Example
GET /api/v1/sub-accounts/5caefba7d9575a0688f83c45

### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.

### Parameters

Param | Type | Description
--------- | ------- | ------- 
subUserId | String | the [user ID](#get-user-info-of-all-sub-accounts) of a sub-account.

### RESPONSES

Field | Description
--------- | ------- 
subUserId | The user ID of a sub-user.
subName | The username of a sub-user.
currency | Currency
balance | Total funds in an account.
available | Funds available to withdraw or trade.
holds | Funds on hold (not available for use).
baseCurrency | Calculated on this currency.
baseCurrencyPrice | The base currency price.
baseAmount | The base currency amount.
 

## Get the Aggregated Balance of all Sub-Accounts


```json
[
  {
		"subUserId": "5caefba7d9575a0688f83c45",
		"subName": "kucoin1",
		"mainAccounts": [{
			"currency": "BTC",
			"balance": "6",
			"available": "6",
      "holds": "0",
      "baseCurrency": "BTC",
      "baseCurrencyPrice": "1",
      "baseAmount": "1.1"

		}],
		"tradeAccounts": [{
			"currency": "BTC",
			"balance": "1000",
			"available": "1000",
      "holds": "0",
      "baseCurrency": "BTC",
      "baseCurrencyPrice": "1",
      "baseAmount": "1.1"
    }],
    "marginAccounts": [{
        "currency": "BTC",
        "balance": "1.1",
        "available": "1.1",
        "holds": "0",
        "baseCurrency": "BTC",
        "baseCurrencyPrice": "1",
        "baseAmount": "1.1"
    }]
  }
]
```

This endpoint returns the account info of all sub-users.

### HTTP REQUEST

**GET /api/v1/sub-accounts**

### Example
GET /api/v1/sub-accounts

### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.

### RESPONSES

Field | Description
--------- | ------- 
subUserId | The user ID of the sub-user.
subName | The username of the sub-user.
currency | The currency of the account.
balance | Total funds in the account.
available | Funds available to withdraw or trade.
holds | Funds on hold (not available for use).
baseCurrency | Calculated on this currency.
baseCurrencyPrice | The base currency price.
baseAmount | The base currency amount.
 

## Get the Transferable Balance

```json
 {
    "currency": "KCS",
    "balance": "0",
    "available": "0",
    "holds": "0",
    "transferable": "0"
}
```
This endpoint returns the transferable balance of a specified account.


### HTTP REQUEST
**GET /api/v1/accounts/transferable**

### Example
GET /api/v1/accounts/transferable?currency=BTC&type=MAIN

### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.

### Parameters

Param | Type | Description
--------- | ------- | ------- 
currency | String | [currency](#Get-Currencies)
type | String | The account type: **MAIN**, **TRADE** or **MARGIN**


### RESPONSES

Field | Description
--------- | ------- 
currency | Currency
balance | Total funds in an account.
available | Funds available to withdraw or trade.
holds | Funds on hold (not available for use).
transferable | Funds available to transfer.


## Transfer between Master user and Sub-user


```json
{
	"orderId": "5cbd870fd9575a18e4438b9a"
}
```
This endpoint is used for transferring the assets between the master user and the sub-user.<br/> The main account of the master user supports the transfer to the main account or trade account of the sub-user. 




### HTTP REQUEST

**POST /api/v1/accounts/sub-transfer**

### Example
POST /api/v1/accounts/sub-transfer


### API KEY PERMISSIONS
This endpoint requires the **"Trade"** permission.

### Parameters

Param | Type | Description
--------- | ------- | ------- 
clientOid | String | Unique order id created by users to identify their orders, e.g. UUID.
currency | String | [currency](#Get-Currencies)
amount | String | Transfer amount, the amount is a positive integer multiple of the [currency precision](#get-currencies).
direction | String | OUT — the master user to sub user<br/>IN — the sub user to the master user.
accountType | String | *[Optional]* The account type of the master user: **MAIN**
subAccountType | String | The account type of the sub user: **MAIN**, **TRADE** or **MARGIN**
subUserId | String | the [user ID](#get-user-info-of-all-sub-accounts) of a sub-account.


### RESPONSES

Field | Description
--------- | ------- 
orderId | The order ID of a master-sub assets transfer.
 



## Inner Transfer

```json
{
    "orderId": "5bd6e9286d99522a52e458de"
}
```

The inner transfer interface is used for transferring assets between the accounts of a user and is free of charges. For example, a user could transfer assets from their main account to their trading account on the platform. 

### HTTP REQUEST

**POST /api/v2/accounts/inner-transfer**

### Example
POST /api/v2/accounts/inner-transfer

### API KEY PERMISSIONS
This endpoint requires the **"Trade"** permission.
  
### Parameters

Param | Type | Description
--------- | ------- | ------- 
clientOid | String | Unique order id created by users to identify their orders, e.g. UUID.
currency | String | [currency](#Get-Currencies)
from | String | Account type of payer: **main**, **trade** or **margin** 
to | String | Account type of payee: **main**, **trade** or **margin** 
amount | String | Transfer amount, the amount is a positive integer multiple of the [currency precision](#get-currencies).


### RESPONSES
Field | Description
--------- | ------- 
orderId | The order ID of a funds transfer




# Deposit

## Create Deposit Address

```json
{
	"address": "0x78d3ad1c0aa1bf068e19c94a2d7b16c9c0fcd8b1",
	"memo": "5c247c8a03aa677cea2a251d",   //tag
	"chain": "OMNI"
}
```
Request via this endpoint to create a deposit address for a currency you intend to deposit. 

###HTTP REQUEST
**POST /api/v1/deposit-addresses**

### Example
POST /api/v1/deposit-addresses

### API KEY PERMISSIONS
This endpoint requires the **"Transfer"** permission.

### Parameters

Param | Type | Description
--------- | ------- | -----------
currency | String | Currency
chain | String | *[Optional]* The chain name of currency, e.g. The available value for USDT are OMNI, ERC20, TRC20, default is OMNI. This only apply for multi-chain currency, and there is no need for single chain currency.

### RESPONSES
Field | Description
--------- | ------- | -----------
address | Deposit address
memo | Address remark. If there’s no remark, it is empty. When you [withdraw](#apply-withdraw) from other platforms to the KuCoin, you need to fill in memo(tag). If you do not fill memo (tag), your deposit may not be available, please be cautious.
chain | The chain name of currency, e.g. The available value for USDT are OMNI, ERC20, TRC20, default is OMNI. 

## Get Deposit Address

```json
{
	"address": "0x78d3ad1c0aa1bf068e19c94a2d7b16c9c0fcd8b1",
	"memo": "5c247c8a03aa677cea2a251d",        //tag
	"chain": "OMNI"
}
```

Get a deposit address for the currency you intend to deposit. If the returned data is null, you may need to create a deposit address first.

###HTTP REQUEST
**GET /api/v1/deposit-addresses**

### Example
GET /api/v1/deposit-addresses

### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.

### Parameters

Param | Type | Description
--------- | ------- | -----------
currency | String | Currency 
chain | String | *[Optional]* The chain name of currency, e.g. The available value for USDT are OMNI, ERC20, TRC20, default is OMNI. This only apply for multi-chain currency, and there is no need for single chain currency.

### RESPONSES
Field | Description
--------- | ------- | -----------
address | Deposit address
memo | Address remark. If there’s no remark, it is empty. When you [withdraw](#apply-withdraw) from other platforms to the KuCoin, you need to fill in memo(tag). If you do not fill memo (tag), your deposit may not be available, please be cautious.
chain | The chain name of currency, e.g. The available value for USDT are OMNI, ERC20, TRC20, default is OMNI.


## Get Deposit List

```json
{
  "currentPage": 1,
  "pageSize": 5,
  "totalNum": 2,
  "totalPage": 1,
	"items": [{
		"address": "0x5f047b29041bcfdbf0e4478cdfa753a336ba6989",
		"memo": "5c247c8a03aa677cea2a251d",   
		"amount": 1,
		"fee": 0.0001,
		"currency": "KCS",
		"isInner": false,
		"walletTxId": "5bbb57386d99522d9f954c5a@test004",
		"status": "SUCCESS",
        "remark": "test",
		"createdAt": 1544178843000,
		"updatedAt": 1544178891000
	}, {
		"address": "0x5f047b29041bcfdbf0e4478cdfa753a336ba6989",
		"memo": "5c247c8a03aa677cea2a251d",
		"amount": 1,
		"fee": 0.0001,
		"currency": "KCS",
		"isInner": false,
		"walletTxId": "5bbb57386d99522d9f954c5a@test003",
		"status": "SUCCESS",
        "remark": "test",
		"createdAt": 1544177654000,
		"updatedAt": 1544178733000
	}]
}
```

Request via this endpoint to get deposit list
Items are paginated and sorted to show the latest first. See the [Pagination](#pagination) section for retrieving additional entries after the first page.


###HTTP REQUEST
**GET /api/v1/deposits**

### Example
GET /api/v1/deposits

### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.

<aside class="notice">This request is paginated.</aside>

### Parameters

Param | Type | Description
--------- | ------- | -----------
currency | String | *[Optional]*  Currency 
startAt| long | *[Optional]*  Start time (milisecond)
endAt| long | *[Optional]* End time (milisecond)
status | String | *[Optional]*  Status. Available value: PROCESSING, SUCCESS, and FAILURE

### RESPONSES
Field | Description
--------- | ------- | -----------
address | Deposit address
memo |Address remark. If there’s no remark, it is empty. When you [withdraw](#apply-withdraw) from other platforms to the KuCoin, you need to fill in memo(tag). If you do not fill memo (tag), your deposit may not be available, please be cautious.
amount | Deposit amount
fee | Fees charged for deposit
currency | Currency
isInner | Internal deposit or not
walletTxId | Wallet Txid
status | Status
remark | remark
createdAt | Creation time of the database record
updatedAt | Update time of the database record



## Get V1 Historical Deposits List

```json
{
"currentPage": 1,
"pageSize": 1,
"totalNum": 9,
"totalPage": 9,
"items": [{
"currency": "BTC",
"createAt": 1528536998,
"amount": "0.03266638",
"walletTxId": "55c643bc2c68d6f17266383ac1be9e454038864b929ae7cee0bc408cc5c869e8@12ffGWmMMD1zA1WbFm7Ho3JZ1w6NYXjpFk@234",
"isInner": false,
"status": "SUCCESS"
}]
}
```

Request via this endpoint to get the V1 historical deposits list on KuCoin.
<aside class="notice">The data of the latest one month will be queried by default.</aside>

###HTTP REQUEST
**GET /api/v1/hist-deposits**

### Example
GET /api/v1/hist-deposits

### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.

<aside class="notice">This request is paginated.</aside>

### Parameters

Param | Type | Description
--------- | ------- | -----------
currency | String | *[Optional]*  [Currency](#get-currencies).
startAt| long | *[Optional]*  Start time (milisecond)
endAt| long | *[Optional]* End time (milisecond)
status | String | *[Optional]*  Status. Available value: PROCESSING, SUCCESS, and FAILURE

### RESPONSES
Field | Description
--------- | ------- | -----------
amount | Deposit amount
currency | Currency
isInner | Internal deposit or not
walletTxId | Wallet Txid
createAt | Creation time of the database record
status | Status




# Withdrawals


## Get Withdrawals List

```json
{
  "currentPage": 1,
  "pageSize": 10,
  "totalNum": 1,
  "totalPage": 1,
	"items": [{
	  "id": "5c2dc64e03aa675aa263f1ac",
		"address": "0x5bedb060b8eb8d823e2414d82acce78d38be7fe9",
		"memo": "",
		"currency": "ETH",
		"amount": 1.0000000,
    "fee": 0.0100000,
		"walletTxId": "3e2414d82acce78d38be7fe9",
		"isInner": false,
		"status": "FAILURE",
      "remark": "test",
		"createdAt": 1546503758000,
		"updatedAt": 1546504603000
	}]
}
```

###HTTP REQUEST
**GET /api/v1/withdrawals**

### Example
GET /api/v1/withdrawals

### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.

<aside class="notice">This request is paginated.</aside>

### Parameters

Param | Type | Description
--------- | ------- | -----------
currency | String | *[Optional]*  [Currency](#get-currencies)
status | String | *[Optional]*  Status. Available value: PROCESSING, WALLET_PROCESSING, SUCCESS, and FAILURE
startAt| long | *[Optional]*  Start time (milisecond)
endAt| long | *[Optional]* End time (milisecond)

### RESPONSES
Field | Description
--------- | ------- 
id | Unique identity 
address | Withdrawal address
memo |  Address remark. If there’s no remark, it is empty. When you [withdraw](#apply-withdraw) from other platforms to the KuCoin, you need to fill in memo(tag). If you do not fill memo (tag), your deposit may not be available, please be cautious.
currency | Currency 
amount | Withdrawal amount
fee | Withdrawal fee 
walletTxId | Wallet Txid
isInner | Internal withdrawal or not
status | status 
remark | remark
createdAt | Creation time
updatedAt | Update time




## Get V1 Historical Withdrawals List

```json
{
"currentPage": 1,
"pageSize": 1,
"totalNum": 2,
"totalPage": 2,
"items": [{
"currency": "BTC",
"createAt": 1526723468,
"amount": "0.534",
"address": "33xW37ZSW4tQvg443Pc7NLCAs167Yc2XUV",
"walletTxId": "aeacea864c020acf58e51606169240e96774838dcd4f7ce48acf38e3651323f4",
"isInner": false,
"status": "SUCCESS"
}]
}
```
List of KuCoin V1 historical withdrawals.

<aside class="notice">Default query for one month of data.</aside>

###HTTP REQUEST
**GET /api/v1/hist-withdrawals**

### Example
GET /api/v1/hist-withdrawals


### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.

<aside class="notice">This request is paginated.</aside>

### Parameters

Param | Type | Description
--------- | ------- | -----------
currentPage | int | *[Optional]*  The current page.
pageSize | int | *[Optional]*  Number of entries per page.  
currency | String | *[Optional]*  [Currency](#get-currencies).
startAt| long | *[Optional]*  Start time (milisecond)
endAt| long | *[Optional]* End time (milisecond)
status | String | *[Optional]*  Status. Available value: PROCESSING, SUCCESS, and FAILURE

### RESPONSES
Field | Description
--------- | ------- | -----------
amount | Withdrawal amount
currency | Currency
isInner | Internal deposit or not
walletTxId | Wallet Txid
createAt | Creation time of the database record
status | Status




##  Get Withdrawal Quotas

```json
{
	"currency": "KCS",
	"limitBTCAmount": "2.0",
	"usedBTCAmount": "0",
	"limitAmount": "75.67567568",
	"remainAmount": "75.67567568",
	"availableAmount": "9697.41991348",
	"withdrawMinFee": "0.93000000",
	"innerWithdrawMinFee": "0.00000000",
	"withdrawMinSize": "1.4",
	"isWithdrawEnabled": true,
	"precision": 8,   //withdrawal precision
	"chain": "OMNI"
}
```

###HTTP REQUEST
**GET /api/v1/withdrawals/quotas**

### Example
GET /api/v1/withdrawals/quotas?currency=BTC


### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.

### Parameters

Param | Type | Description
--------- | ------- | -----------
currency | String | currency. e.g. BTC
chain | String | *[Optional]* The chain name of currency, e.g. The available value for USDT are OMNI, ERC20, TRC20, default is OMNI. This only apply for multi-chain currency, and there is no need for single chain currency.

### RESPONSES
Field | Description
--------- | ------- | -----------
currency | Currency
availableAmount | Current available withdrawal amount
remainAmount | Remaining amount available to withdraw the current day
withdrawMinSize | Minimum withdrawal amount
limitBTCAmount | Total BTC amount available to withdraw the current day
innerWithdrawMinFee | Fees for internal withdrawal
usedBTCAmount | The estimated BTC amount (based on the daily fiat limit) that can be withdrawn within the current day
isWithdrawEnabled | Is the withdraw function enabled or not
withdrawMinFee | Minimum withdrawal fee
precision | Floating point precision. 
chain | The chain name of currency, e.g. The available value for USDT are OMNI, ERC20, TRC20, default is OMNI.

## Apply Withdraw

```json
{
  "withdrawalId": "5bffb63303aa675e8bbe18f9"
}
```

###HTTP REQUEST
**POST /api/v1/withdrawals**

<aside class="notice">On the WEB end, you can open the switch of specified favorite addresses for withdrawal, and when it is turned on, it will verify whether your withdrawal address is a favorite address.</aside>

### Example
POST /api/v1/withdrawals

### API KEY PERMISSIONS
This endpoint requires the **"Transfer"** permission.

### Parameters

Param | Type | Description
--------- | ------- | -----------
currency  | String | Currency
address   | String | Withdrawal address
amount | number | Withdrawal amount, a positive number which is a multiple of the amount precision (fees excluded) 
memo   | String | *[Optional]*   Address remark. If there’s no remark, it is empty. When you withdraw from other platforms to the KuCoin, you need to fill in memo(tag). If you do not fill memo (tag), your deposit may not be available, please be cautious.
isInner | boolean | *[Optional]*  Internal withdrawal or not. Default setup: false
remark | String | *[Optional]*  Remark
chain | String | *[Optional]* The chain name of currency, e.g. The available value for USDT are OMNI, ERC20, TRC20, default is OMNI. This only apply for multi-chain currency, and there is no need for single chain currency.

### RESPONSES
Field | Description
--------- | ------- 
withdrawalId | Withdrawal id

For cryptocurrency withdrawal, KuCoin supports internal and external transaction fee deduction, which means when the balance in your main account is sufficient to support the withdrawal, the system will initially deduct the transaction fees from your main account. But if the balance in your main account is not sufficient to support the withdrawal, the system will deduct the fees from your withdrawal amount.

For example:

Suppose you are going to withdraw 1 BTC from the KuCoin platform (transaction fee: 0.0001BTC), if the balance in your main account is insufficient, the system will deduct the transaction fees from your withdrawal amount. In this case, you will be receiving 0.9999BTC.

## Cancel Withdrawal

Only withdrawals requests of **PROCESSING** status could be canceled.

###HTTP REQUEST
**DELETE /api/v1/withdrawals/{withdrawalId}**

### Example
DELETE /api/v1/withdrawals/5bffb63303aa675e8bbe18f9

### API KEY PERMISSIONS
This endpoint requires the **"Transfer"** permission.

### Parameters

Param | Type | Description
--------- | ------- | -----------
withdrawalId | String | Path parameter, a unique ID for a withdrawal order 

# Trade

Signature is required for this part.

# Orders

## Place a new order

```json
{
  "orderId": "5bd6e9286d99522a52e458de"
}
```

You can place two types of orders: **limit** and **market**. Orders can only be placed if your account has sufficient funds. Once an order is placed, your account funds will be put on hold for the duration of the order. How much and which funds are put on hold depends on the order type and parameters specified. See the Holds details below. 

Please note that the system will deduct the fees from the orders that entered the order book in advance. Read [List Fills](#list-fills) to learn more.

Before placing an order, please read [Get Symbol List](#get-symbols-list) to understand the requirements for the quantity parameters for each trading pair.

**Do not include extra spaces in JSON strings**.

###Place Order Limit

The maximum matching orders for a single trading pair in one account is **200** (stop orders included). 


### HTTP Request
**POST /api/v1/orders**

### Example
POST /api/v1/orders


### API KEY PERMISSIONS
This endpoint requires the **"Trade"** permission.

### Parameters

| Param     | type   | Description  |
| --------- | ------ |-------------------------------- |
| clientOid | String | Unique order id created by users to identify their orders, e.g. UUID. |
| side      | String | **buy** or **sell**      |
| symbol    | String | a valid trading symbol code. e.g. ETH-BTC     |
| type      | String | *[Optional]* **limit** or **market** (default is **limit**)          |
| remark    | String | *[Optional]*  remark for the order, length cannot exceed 100 utf8 characters|
| stop      | String | *[Optional]* Either **loss** or **entry**. Requires **stopPrice** to be defined |
| stopPrice | String | *[Optional]* Need to be defined if stop is specified. |
| stp       | String | *[Optional]*  self trade prevention , **CN**, **CO**, **CB** or **DC**|

#### LIMIT ORDER PARAMETERS

| Param       | type    | Description                                                  |
| ----------- | ------- | ------------------- |
| price       | String  | price per base currency          |
| size        | String  | amount of base currency to buy or sell         |
| timeInForce | String  | *[Optional]* **GTC**, **GTT**, **IOC**, or **FOK** (default is **GTC**), read [Time In Force](#time-in-force).   |
| cancelAfter | long    | *[Optional]*  cancel after **n** seconds, requires **timeInForce** to be **GTT**                   |
| postOnly    | boolean | *[Optional]*  Post only flag, invalid when **timeInForce** is **IOC** or **FOK**                               |
| hidden      | boolean | *[Optional]*  Order will not be displayed in the order book |
| iceberg    | boolean | *[Optional]*  Only aportion of the order is displayed in the order book |
| visibleSize | String  | *[Optional]*  The maximum visible size of an iceberg order   |


#### MARKET ORDER PARAMETERS

Param | type | Description
--------- | ------- | -----------
size | String | *[Optional]*  Desired amount in base currency
funds | String | *[Optional]*  The desired amount of quote currency to use

* It is required that you use one of the two parameters, **size** or **funds**.

###Advanced Description

###SYMBOL

The symbol must match a valid trading [symbol](#get-symbols-list).

###CLIENT ORDER ID

Generated by yourself, the optional clientOid field must be a unique id (e.g UUID). Only numbers, characters, underline(_) and separator(-) are allowed. The value will be returned in order detail. You can use this field to identify your orders via the public feed. The client_oid is different from the server-assigned order id. Please do not send a repeated client_oid. The length of the client_oid cannot exceed 40 characters. You should record the server-assigned order_id as it will be used for future query order status.


###TYPE

The order type you specify may decide whether other optional parameters are required, as well as how your order will be executed by the matching engine. If order type is not specified, the order will be a **limit** order by default.

**Price** and **size** are required to be specified for a **limit order**.  The order will be filled at the price specified or better, depending on the market condition.   If a limit order cannot be filled immediately, it will be outstanding in the open order book until matched by another order, or canceled by the user.


A **market order** differs from a limit order in that the execution price is not guaranteed. Market order, however, provides a way to buy or sell specific size of order without having to specify the price. Market orders will be executed immediately, and no orders will enter the open order book afterwards. Market orders are always considered takers and incur taker fees.



###STOP ORDER

A stop order is an order to buy or sell the specified amount of cryptos at the last traded
price or pre-specified limit price once the order has traded at or through a pre-specified stopPrice. The order will be executed by the highest price first. For orders of the same price, the order will be executed in time priority.

**stop: 'loss':** Triggers when the last trade price changes to a value at or below the stopPrice.

**stop: 'entry':** Triggers when the last trade price changes to a value at or above the stopPrice.


The last trade can be found in the latest match message. Note that not all match messages may be received due to dropped messages.

The last trade price is the last price at which an order was filled. This price can be found in the latest match message. Note that not all match messages may be received due to dropped messages.

Note that when triggered, stop orders execute as either market or limit orders, depending on the type. 

When placing a stop loss order, the system will pre-freeze the assets in your account for the order. **When you are going to place a stop market order, we recommend you to specify the funds for the order when trading**.

###PRICE
The price must be specified in priceIncrement symbol units. The priceIncrement is the smallest unit of price. For the BTC-USDT symbol, the priceIncrement is 0.00001000. Prices less than 0.00001000 will not be accepted, The price for the placed order should be multiple numbers of priceIncrement, or the system would report an error when you place the order. Not required for market orders. 

###SIZE
The size must be greater than the baseMinSize for the symbol and no larger than the baseMaxSize. The size must be specified in baseIncrement symbol units. Size indicates the amount of BTC (or base currency) to buy or sell.

###FUNDS
The funds field indicates the how much of the quote currency you wish to buy or sell. The size of the funds must be specified in quoteIncrement symbol units and the size of funds in order shall be a positive integer multiple of quoteIncrement, ensuring the funds is greater than the quoteMinSize for the symbol but no larger than the quoteMaxSize.


###TIME IN FORCE
Time in force policies provide guarantees about the lifetime of an order. There are four policies: Good Till Canceled **GTC**, Good Till Time **GTT**, Immediate Or Cancel **IOC**, and Fill Or Kill **FOK**.

**GTC** Good Till Canceled orders remain open on the book until canceled. This is the default behavior if no policy is specified.

**GTT** Good Till Time orders remain open on the book until canceled or the allotted cancelAfter is depleted on the matching engine. GTT orders are guaranteed to cancel before any other order is processed after the cancelAfter seconds placed in order book.

**IOC** Immediate Or Cancel orders instantly cancel the remaining size of the limit order instead of opening it on the book.

**FOK** Fill Or Kill orders are rejected if the entire size cannot be matched.

* Note that self trades belong to match as well.

###POST ONLY
The post-only flag ensures that the trader always pays the maker fee and provides liquidity to the order book. If any part of the order is going to pay taker fee, the order will be fully rejected.

If a post only order will get executed immediately against the existing orders (except iceberg and hidden orders) in the market, the order will be cancelled. If the post only order will execute against an iceberg/hidden order immediately, you will get the maker fees.

 **Notice**: The post only order cannot to be placed simultaneously with an iceberg order or hidden order. 


### HIDDEN AND ICEBERG


The **Hidden** and **iceberg Orders** are two **options** in advanced settings (note: the iceberg order is a special form of the hidden order). You may select “Hidden” or “Iceberg” when placing a limit or stop limit order.

A hidden order will enter but not display on the orderbook.

Different from the hidden order, an **iceberg order** is divided into visible portion and invisible portion. When placing an iceberg order, you need to set the **visible size**. The minimum visible size is 1/20 of the order size. The minimum visible size shall be greater than the minimum order size, or an error will occur.

In a matching event, the visible portion of an iceberg order will be executed first, and another visible portion will pop up until the order is fully filled.

**Note**: 
- The system will charge **taker fees** for **Hidden** and **iceberg Orders**. 

- If both "Iceberg" and "Hidden" are selected, your order will be filled as an **iceberg Order** by default.


###HOLDS
For limit buy orders, we will hold the needed portion from your funds (price x size of the order). Likewise, on sell orders, we will also hold the amount of assets that you wish to sell. Actual fees are assessed at the time of a trade. If you cancel a partially filled or unfilled order, any remaining funds will be released from being held.

For market buy or sell orders where the funds are specified, the funds amount will be put on hold. If only size is specified, all of your account balance (in the quote account) will be put on hold for the duration of the market order (usually a trivially short time). 

###SELF-TRADE PREVENTION

**Self-Trade Prevention** is an option in advanced settings.It is not selected by default. If you specify **STP** when placing orders, your order won't be matched by another one which is also yours. On the contrary, if **STP** is not specified in advanced, your order can be matched by another one of your own orders.

**Market order is currently not supported for DC**. When the **timeInForce** is set to **FOK**, the **stp** flag will be forcely specified as **CN**.


**Market order is currently not supported for DC**. When *timeInForce* is **FOK**, the stp flag will be forced to be specified as **CN**.

| Flag | Name                          |
| ---- | ----------------------------- |
| DC   | Decrease and Cancel           |
| CO   | Cancel oldest                 |
| CN   | Cancel newest                 |
| CB   | Cancel both                   |

###ORDER LIFECYCLE
The HTTP Request will respond when an order is either rejected (insufficient funds, invalid parameters, etc) or received (accepted by the matching engine). A **200** response indicates that the order was received and is active. **Active** orders may execute immediately (depending on price and market conditions) either partially or fully. A partial execution will put the remaining size of the order in the open state. An order that is filled completely, will go into the **done** state.

Users listening to streaming market data are encouraged to use the order ID field to identify their received messages in the feed.


###RESPONSES
Field | Description
--------- | ------- 
orderId | The ID of the order

A successful order will be assigned an order ID. A successful order is defined as one that has been accepted by the matching engine.

<aside class="notice">Open orders do not expire and will remain open until they are either filled or canceled.</aside>

## Cancel an order

```json
{
     "cancelledOrderIds": [
      "5bd6e9286d99522a52e458de"   //orderId
    ]
}
```

Request via this endpoint to cancel a single order previously placed.

You will receive cancelledOrderIds field once the system has received the cancellation request. The cancellation request will be processed by the matching engine in sequence. To know if the request is processed    (successfully or not), you may check the order status or the update message from the pushes.


### HTTP REQUEST 
**DELETE /api/v1/orders/{orderId}**

### Example
DELETE /api/v1/orders/5bd6e9286d99522a52e458de


### API KEY PERMISSIONS 
This endpoint requires the **"Trade"** permission.

### Parameters ###
Param | Type | Description
--------- | ------- | -----------
orderId | String | [Order ID](#list-orders), unique ID of the order.

###RESPONSES###
Field | Description
--------- | ------- 
orderId | Unique ID of the cancelled order



<aside class="notice">The <b>order ID</b> is the server-assigned order id and not the passed clientOid.</aside>

### CANCEL REJECT ###
If the order could not be canceled (already filled or previously canceled, etc), then an error response will indicate the reason in the **message** field.

## Cancel all orders

```json
{
   "cancelledOrderIds": [
      "5c52e11203aa677f33e493fb",  //orderId
      "5c52e12103aa677f33e493fe",
      "5c52e12a03aa677f33e49401",
      "5c52e1be03aa677f33e49404",
      "5c52e21003aa677f33e49407",
      "5c6243cb03aa67580f20bf2f",
      "5c62443703aa67580f20bf32",
      "5c6265c503aa676fee84129c",
      "5c6269e503aa676fee84129f",
      "5c626b0803aa676fee8412a2"
    ]
}
```

Request via this endpoint to cancel all open orders. The response is a list of ids of the canceled orders.

###HTTP REQUEST
**DELETE /api/v1/orders**

### Example
**DELETE /api/v1/orders?symbol=ETH-BTC**

### API KEY PERMISSIONS
This endpoint requires the **"Trade"** permission.

### Parameters
Param | Type | Description
--------- | ------- | -----------
symbol | String | *[Optional]* symbol, cancel the orders for the specified trade pair. 

###RESPONSES###
Field | Description
--------- | ------- 
orderId | Order ID, unique identifier of an order. 



## List Orders

```json
{
    "currentPage": 1,
    "pageSize": 1,
    "totalNum": 153408,
    "totalPage": 153408,
    "items": [
      {
        "id": "5c35c02703aa673ceec2a168",   //orderid
        "symbol": "BTC-USDT",   //symbol
        "opType": "DEAL",      // operation type,deal is pending order,cancel is cancel order
        "type": "limit",       // order type,e.g. limit,market,stop_limit.
        "side": "buy",         // transaction direction,include buy and sell
        "price": "10",         // order price
        "size": "2",           // order quantity
        "funds": "0",          // order funds
        "dealFunds": "0.166",  // deal funds
        "dealSize": "2",       // deal quantity
        "fee": "0",            // fee
        "feeCurrency": "USDT", // charge fee currency
        "stp": "",             // self trade prevention,include CN,CO,DC,CB
        "stop": "",            // stop type
        "stopTriggered": false,  // stop order is triggered
        "stopPrice": "0",      // stop price
        "timeInForce": "GTC",  // time InForce,include GTC,GTT,IOC,FOK
        "postOnly": false,     // postOnly
        "hidden": false,       // hidden order
        "iceberg": false,      // iceberg order
        "visibleSize": "0",    // display quantity for iceberg order
        "cancelAfter": 0,      // cancel orders time，requires timeInForce to be GTT
        "channel": "IOS",      // order source
        "clientOid": "",       // user-entered order unique mark
        "remark": "",          // remark
        "tags": "",            // tag order source        
        "isActive": false,     // status before unfilled or uncancelled 
        "cancelExist": false,   // order cancellation transaction record
        "createdAt": 1547026471000  // create time
      }
    ]
 }
```

Request via this endpoint to get your current order list. Items are paginated and sorted to show the latest first. See the [Pagination](#pagination) section for retrieving additional entries after the first page.

### HTTP REQUEST
**GET /api/v1/orders**

### Example
GET /api/v1/orders?status=active

### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.

<aside class="notice">This request is paginated.</aside>


###PARAMETERS
You can pinpoint the results with the following query paramaters.

Param | Type | Description
--------- | ------- | -----------
status | String |*[Optional]* **active** or **done**(done as default), Only list orders with a specific status .
symbol |String|*[Optional]* Only list orders for a specific symbol.
side | String | *[Optional]* **buy** or **sell** 
type | String | *[Optional]* **limit**, **market**, **limit_stop** or **market_stop** 
startAt| long | *[Optional]*  Start time (milisecond)
endAt| long | *[Optional]* End time (milisecond)

###RESPONSES
Field | Description
--------- | ------- 
id |  Order ID, the ID of an order.
symbol | symbol
opType |  operation type, Deal (status of the pending orders) and Cancel (status of the canceled orders)
type | order type,e.g. limit,market,stop_limit.
side | transaction direction,include buy and sell
price |  order price
size |  order quantity
funds | order funds
dealFunds |  executed size of funds
dealSize | executed quantity
fee | fee
feeCurrency | charge fee currency
stp |  self trade prevention,include CN,CO,DC,CB
stop |  stop type, include entry and loss
stopTriggered |  stop order is triggered or not
stopPrice |  stop price
timeInForce | time InForce,include GTC,GTT,IOC,FOK
postOnly | postOnly
hidden | hidden order
iceberg | iceberg order
visibleSize | displayed quantity for iceberg order
cancelAfter | cancel orders time，requires timeInForce to be GTT
channel | order source
clientOid | user-entered order unique mark
remark | remark
tags | tag order source
isActive |  order status, true and false. If true, the order is active, if false, the order is fillled or cancelled 
cancelExist | order cancellation transaction record
createdAt | create time


###ORDER STATUS AND SETTLEMENT
Any order on the exchange order book is in active status. Orders removed from the order book will be marked with done status. After an order becomes done, there may be a few milliseconds latency before it’s fully settled.

You can check the orders in any status. If the status parameter is not specified, orders of done status will be returned by default.

When you query orders in active status, there is no time limit. However, when you query orders in done status, the start and end time range cannot exceed 7* 24 hours. An error will occur if the specified time window exceeds the range. If you specify the end time only, the system will automatically calculate the start time as end time minus 7*24 hours, and vice versa.


The history for cancelled orders is only kept for **one month**. You will not be able to query for cancelled orders that have happened more than a month ago.

<aside class="notice">The total number of items retrieved cannot exceed 500,000. If it is exceeded, please shorten the query time range.</aside>

###POLLING
For high-volume trading, it is highly recommended that you maintain your own list of open orders and use one of the streaming market data feeds to keep it updated. You should poll the open orders endpoint to obtain the current state of any open order.



## Get V1 Historical Orders List

```json
{
	"currentPage": 1,
	"pageSize": 50,
	"totalNum": 1,
	"totalPage": 1,
	"items": [{
		"symbol": "SNOV-ETH",
		"dealPrice": "0.0000246",
		"dealValue": "0.018942",
		"amount": "770",
		"fee": "0.00001137",
		"side": "sell",
		"createdAt": 1540080199
	}]
}
```

Request via this endpoint to get your historical orders list of the KuCoin V1. 
Items are paginated and sorted to show the latest first. See the [Pagination](#pagination) section for retrieving additional entries after the first page.

<aside class="notice">Default query for one month of data.</aside>

###HTTP REQUEST
**GET /api/v1/hist-orders**

### Example
GET /api/v1/hist-orders

### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.

<aside class="notice">This request is paginated.</aside>


###PARAMETERS
You can request for specific orders using query parameters.

Param | Type | Description
--------- | ------- | -----------
currentPage | int | *[Optional]*  The current page.
pageSize | int | *[Optional]*  Number of entries per page.  
symbol | String | *[Optional]* a valid trading [symbol code](#get-symbols-list). e.g. ETH-BTC.
startAt| long | *[Optional]*  Start time (milisecond)
endAt| long | *[Optional]* End time (milisecond)
side | String | *[Optional]*  **buy** or **sell**

###RESPONSES###
Field | Description
--------- | -------
symbol | symbol
dealPrice | Filled price
dealValue | Executed size of funds
side | transaction direction,include buy and sell.
amount |   Executed quantity
size |  Order quantity.
fee | Fee.
createdAt | Create time.



## Recent Orders

```json
{
    "currentPage": 1,
    "pageSize": 1,
    "totalNum": 153408,
    "totalPage": 153408,
    "items": [
      {
        "id": "5c35c02703aa673ceec2a168",
        "symbol": "BTC-USDT",
        "opType": "DEAL",
        "type": "limit",
        "side": "buy",
        "price": "10",
        "size": "2",
        "funds": "0",
        "dealFunds": "0.166",
        "dealSize": "2",
        "fee": "0",
        "feeCurrency": "USDT",
        "stp": "",
        "stop": "",
        "stopTriggered": false,
        "stopPrice": "0",
        "timeInForce": "GTC",
        "postOnly": false,
        "hidden": false,
        "iceberg": false,
        "visibleSize": "0",
        "cancelAfter": 0,
        "channel": "IOS",
        "clientOid": "",
        "remark": "",
        "tags": "",
        "isActive": false,
        "cancelExist": false,
        "createdAt": 1547026471000
      }
    ]
 }
```

Request via this endpoint to get 1000 orders in the last 24 hours. 
Items are paginated and sorted to show the latest first. See the [Pagination](#pagination) section for retrieving additional entries after the first page.

###HTTP REQUEST
**GET /api/v1/limit/orders**

### Example
GET /api/v1/limit/orders

### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.


###RESPONSES
Field | Description
--------- | ------- 
orderId | Order ID, unique identifier of an order. 
symbol | symbol
opType |  operation type,deal is pending order,cancel is cancel order
type | order type,e.g. limit,market,stop_limit.
side | transaction direction,include buy and sell
price |  order price
size |  order quantity
funds | order funds
dealFunds |  deal funds
dealSize | deal quantity
fee | fee
feeCurrency | charge fee currency
stp |  self trade prevention,include CN,CO,DC,CB
stop |  stop type, include entry and loss
stopTriggered |  stop order is triggered
stopPrice |  stop price
timeInForce | time InForce,include GTC,GTT,IOC,FOK
postOnly | postOnly
hidden | hidden order
iceberg | iceberg order
visibleSize | display quantity for iceberg order
cancelAfter | cancel orders time，requires timeInForce to be GTT
channel | order source
clientOid | user-entered order unique mark
remark | remark
tags | tag order source
isActive | order status, true and false. If true, the order is active, if false, the order is fillled or cancelled 
cancelExist | order cancellation transaction record
createdAt | create time



<aside class="spacer4"></aside>
<aside class="spacer2"></aside>

## Get an order

```json
{
    "id": "5c35c02703aa673ceec2a168",
    "symbol": "BTC-USDT",
    "opType": "DEAL",
    "type": "limit",
    "side": "buy",
    "price": "10",
    "size": "2",
    "funds": "0",
    "dealFunds": "0.166",
    "dealSize": "2",
    "fee": "0",
    "feeCurrency": "USDT",
    "stp": "",
    "stop": "",
    "stopTriggered": false,
    "stopPrice": "0",
    "timeInForce": "GTC",
    "postOnly": false,
    "hidden": false,
    "iceberg": false,
    "visibleSize": "0",
    "cancelAfter": 0,
    "channel": "IOS",
    "clientOid": "",
    "remark": "",
    "tags": "",
    "isActive": false,
    "cancelExist": false,
    "createdAt": 1547026471000
 }
```
Request via this endpoint to get a single order info by order ID.

###HTTP REQUEST
**GET /api/v1/orders/{order-id}**

### Example
GET /api/v1/orders/5c35c02703aa673ceec2a168

### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.

###PARAMETERS
Param | Type | Description
--------- | ------- | -----------
orderId | String | Order ID, unique identifier of an order, obtained via the [List orders](#list-orders). 

###RESPONSES
Field | Description
--------- | ------- 
orderId | Order ID, the ID of an order
symbol | symbol
opType |  operation type,deal is pending order,cancel is cancel order
type | order type,e.g. limit,market,stop_limit.
side | transaction direction,include buy and sell
price |  order price
size |  order quantity
funds | order funds
dealFunds |  deal funds
dealSize | deal quantity
fee | fee
feeCurrency | charge fee currency
stp |  self trade prevention,include CN,CO,DC,CB
stop |  stop type, include entry and loss
stopTriggered |  stop order is triggered
stopPrice |  stop price
timeInForce | time InForce,include GTC,GTT,IOC,FOK
postOnly | postOnly
hidden | hidden order
iceberg | iceberg order
visibleSize | display quantity for iceberg order
cancelAfter | cancel orders time，requires timeInForce to be GTT
channel | order source
clientOid | user-entered order unique mark
remark | remark
tags | tag order source
isActive | order status, true and false. If true, the order is active, if false, the order is fillled or cancelled 
cancelExist | order cancellation transaction record
createdAt | create time


<aside class="spacer4"></aside>
<aside class="spacer2"></aside>

# Fills

## List Fills

```json
{
    "currentPage":1,
    "pageSize":1,
    "totalNum":251915,
    "totalPage":251915,
    "items":[
        {
            "symbol":"BTC-USDT",    //symbol
            "tradeId":"5c35c02709e4f67d5266954e",   //trade id
            "orderId":"5c35c02703aa673ceec2a168",   //order id
            "counterOrderId":"5c1ab46003aa676e487fa8e3",  //counter order id
            "side":"buy",   //transaction direction,include buy and sell
            "liquidity":"taker",  //include taker and maker
            "forceTaker":true,  //forced to become taker
            "price":"0.083",   //order price
            "size":"0.8424304",  //order quantity
            "funds":"0.0699217232",  //order funds
            "fee":"0",  //fee
            "feeRate":"0",  //fee rate
            "feeCurrency":"USDT",  // charge fee currency
            "stop":"",        // stop type
            "type":"limit",  // order type,e.g. limit,market,stop_limit.
            "createdAt":1547026472000  //time
        }
    ]
}
```

Request via this endpoint to get the recent fills.

Items are paginated and sorted to show the latest first. See the [Pagination](#pagination) section for retrieving additional entries after the first page.


###HTTP REQUEST
**GET /api/v1/fills**

### Example
GET /api/v1/fills


### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.

<aside class="notice">This request is paginated.</aside>


###PARAMETERS
You can request fills for specific orders using query parameters.

Param | Type | Description
--------- | ------- | -----------
orderId | String |*[Optional]* Limit the list of fills to this orderId（If you specify orderId, ignore other conditions） 
symbol | String |*[Optional]* Limit the list of fills to this symbol 
side | String |*[Optional]* **buy** or **sell** 
type | String |*[Optional]* **limit**, **market**, **limit_stop** or **market_stop** 
startAt| long | *[Optional]*  Start time (milisecond)
endAt| long | *[Optional]* End time (milisecond)

###RESPONSES
Field | Description
--------- | ------- 
symbol | symbol.
tradeId | trade id, it is generated by Matching engine.
orderId | Order ID, unique identifier of an order. 
counterOrderId | counter order id. 
side | transaction direction,include buy and sell.
price |  order price
size |  order quantity
funds | order funds
type | order type,e.g. limit,market,stop_limit.
fee | fee
feeCurrency | charge fee currency
stop |  stop type, include entry and loss
liquidity |  include taker and maker
forceTaker |  forced to become taker, include true and false
createdAt | create time

**Data time range**

The system allows you to retrieve data up to one week (start from the last day by default). If the time period of the queried data exceeds one week (time range from the start time to end time exceeded 7*24 hours), the system will prompt to remind you that you have exceeded the time limit. If you only specified the start time, the system will automatically calculate the end time (end time = start time + 7 * 24 hours). On the contrary, if you only specified the end time, the system will calculate the start time (start time= end time - 7 * 24 hours) the same way.

<aside class="notice">The total number of items retrieved cannot exceed 500,000. If it is exceeded, please shorten the query time range.</aside>

**Settlement**

The settlement contains two parts: 
- **Transactional settlement** 
- **Fee settlement**
  
After an order is matched, the transactional and fee settlement data will be updated in the data store. Once the data is updated, the system would enable the settlement process and will deduct the fees from your pre-frozen assets. After that, the currency will be transferred to the account of the user.  

**Fees**

Orders on KuCoin platform are classified into two types， taker and maker. A taker order matches other resting orders on the exchange order book, and gets executed immediately after order entry. A maker order, on the contrary, stays on the exchange order book and awaits to be matched. Taker orders will be charged taker fees, while maker orders will receive maker rebates. Please note that market orders, iceberg orders and hidden orders are always charged taker fees.

The system will pre-freeze a predicted taker fee when you place an order.The liquidity field indicates if the fill was charged taker or maker fees.

With the leading matching engine system in the market, users placing orders on KuCoin platform are classified into two types: **taker** and **maker**. **Taker**s, as the taker in the market, would be charged with taker fees; while **maker**s as the maker in the market, would be charged with less fees than the taker, or even get maker fees from KuCoin （The exchange platform would compensate the transaction fees for you）. 

After placing orders on the KuCoin platform, to ensure the execution of these orders, the system would pre-freeze your assets based on the taker fee charges (because the system could not predict the order types you may choose). Please be noted that the system would deduct the fees from the orders entered the orderbook in advance.

If your order is market order, the system would charge taker fees from you.

If your order is limit order and is immediately matched and executed, the system would charge **taker fees** from you. On the contrary, if the order or part or your order is not executed immediately and enters into the order book, the system would charge **maker** **fees** from you if it is executed before being cancelled

After the order is executed and when the left order funds is **0**, the transaction is completed. If the remaining funds is not sufficient to support the minimum product (min.: 0.00000001), then the left part in the order would be cancelled.

If your order is a maker order, the system would return the left pre-frozen **taker** fees to you.

Notice: 

- For a **hidden**/**iceberg** order, if it is not executed immediately and becomes a maker order, the system would still charge **taker fees** from you.
- Post Only order will charge you maker fees. If a post only order would get executed immediately against the existing orders (except iceberg and hidden orders) in the market, the order will be cancelled. If the post only order will execute against an iceberg/hidden order immediately, you will get the maker fees. 




For example:

Take **BTC/USDT** as the trading pair, if you plan to buy **1 BTC** in market price, suppose the fee charge is **0.1%** and the data on the order book is as follows:

| Price（USDT） | Size（BTC） | Side |
| ------------- | ----------- | ---- |
| 4200.00       | 0.18412309  | sell |
| 4015.60       | 0.56849308  | sell |
| 4011.32       | 0.24738383  | sell |
| 3995.64       | 0.84738383  | buy  |
| 3988.60       | 0.20484000  | buy  |
| 3983.85       | 1.37584908  | buy  |

 When you placed a buy order in market price, the order would be executed immediately. The transaction detail is as follows:

| Price（USDT） | Size（BTC） | Fee（BTC） |
| ------------- | ----------- | ---------- |
| 4011.32       | 0.24738383  | 0.00024738 |
| 4015.60       | 0.56849308  | 0.00056849 |
| 4200.00       | 0.18312409  | 0.00018312 |




## Recent Fills

```json
{
    "currentPage":1,
    "pageSize":1,
    "totalNum":251915,
    "totalPage":251915,
    "items":[
        {
            "symbol":"BTC-USDT",
            "tradeId":"5c35c02709e4f67d5266954e",
            "orderId":"5c35c02703aa673ceec2a168",
            "counterOrderId":"5c1ab46003aa676e487fa8e3",
            "side":"buy",
            "liquidity":"taker",
            "forceTaker":true,
            "price":"0.083",
            "size":"0.8424304",
            "funds":"0.0699217232",
            "fee":"0",
            "feeRate":"0",
            "feeCurrency":"USDT",
            "stop":"",
            "type":"limit",
            "createdAt":1547026472000
        }
    ]
}
```


Request via this endpoint to get a list of 1000 fills in the last 24 hours.

Items are paginated and sorted to show the latest first. See the [Pagination](#pagination) section for retrieving additional entries after the first page.

###HTTP REQUEST
**GET /api/v1/limit/fills**

### Example
GET /api/v1/limit/fills


### API KEY PERMISSIONS
This endpoint requires the **"General"** permission.

###RESPONSES
Field | Description
--------- | ------- 
symbol | symbol
tradeId | trade id, it is generated by Matching engine.
orderId | Order ID, unique identifier of an order. 
counterOrderId | counter order id. 
side | transaction direction,include buy and sell.
price |  order price
size |  order quantity
funds | order funds
type | order type,e.g. limit,market,stop_limit.
fee | fee
feeCurrency | charge fee currency
stop |  stop type, include entry and loss
liquidity |  include taker and maker
forceTaker |  forced to become taker, include true and false
createdAt | create time



<aside class="spacer4"></aside>
<aside class="spacer2"></aside>

# Market Data

Signature is not required for this part

# Symbols & Ticker

## Get Symbols List

```json
[
  {
    "symbol": "BTC-USDT",
    "name": "BTC-USDT",
    "baseCurrency": "BTC",
    "quoteCurrency": "USDT",
    "baseMinSize": "0.00000001",
    "quoteMinSize": "0.01",
    "baseMaxSize": "10000",
    "quoteMaxSize": "100000",
    "baseIncrement": "0.00000001",
    "quoteIncrement": "0.01",
    "priceIncrement": "0.00000001",
    "feeCurrency": "USDT",
    "enableTrading": true
  }
]
```

Request via this endpoint to get a list of available currency pairs for trading.
If you want to get the market information of the trading symbol, please use [Get All Tickers](#get-all-tickers).

###HTTP REQUEST
**GET /api/v1/symbols**

### Example
GET /api/v1/symbols

###PARAMETERS
You can query all symbols through *market* parameter.

Param | Type | Description
--------- | ------- | -----------
market | String |*[Optional]* The [trading market](#get-market-list).

###RESPONSES

Field |  Description
--------- | -----------
symbol | unique code of a symbol, it would not change after renaming 
name | Name of trading pairs, it would change after renaming 
baseCurrency |  Base currency,e.g. BTC.
quoteCurrency |  Quote currency,e.g. USDT.
baseMinSize |  The minimum order quantity requried to place an order.
quoteMinSize | The minimum order funds required to place a market order.
baseMaxSize |  The maximum order size required to place an order.
quoteMaxSize | The maximum order funds  required to place a market order.
baseIncrement |The increment of the order size. The value shall be a positive multiple of the baseIncrement.
quoteIncrement | The increment of the funds required to place a market order. The value shall be a positive multiple of the quoteIncrement.
priceIncrement |  The increment of the price required to place a limit order. The value shall be a positive multiple of the priceIncrement.
feeCurrency | The currency of charged fees. 
enableTrading |  Available for transaction or not.

The **baseMinSize** and **baseMaxSize** fields define the min and max order size. The **priceIncrement** field specifies the min order price as well as the price increment.This also applies to **quote** currency. 

The order price must be a positive integer multiple of this priceIncrement (i.e. if the increment is 0.01, the  0.001 and 0.021 order prices would be rejected).

**priceIncrement** and **quoteIncrement** may be adjusted in the future. We will notify you by email and site notifications before adjustment.



## Get Ticker

```json
//Get Ticker
{
    "sequence": "1550467636704",
    "bestAsk": "0.03715004",
    "size": "0.17",
    "price": "0.03715005",
    "bestBidSize": "3.803",
    "bestBid": "0.03710768",
    "bestAskSize": "1.788",
    "time": 1550653727731

}
```

Request via this endpoint to get Level 1 Market Data. The returned value includes the best bid price and size, the best ask price and size as well as the last traded price and the last traded size. 

###HTTP REQUEST
**GET /api/v1/market/orderbook/level1**


### Example
GET /api/v1/market/orderbook/level1?symbol=BTC-USDT

###PARAMETERS

Param | Type | Description
--------- | ------- | -----------
symbol | String |[symbol](#get-symbols-list)


### RESPONSES
Field |  Description
--------- | -----------
sequence | Sequence 
bestAsk |  Best ask price
size | Last traded size 
price |  Last traded price 
bestBidSize | Best bid size
bestBid | Best bid price
bestAskSize |  Best ask size
time |  timestamp



<aside class="spacer2"></aside>


## Get All Tickers

```json
{
    "time": 1550653727731,
    "ticker": [
      {
        "symbol": "BTC-USDT",
        "symbolName": "BTC-USDT",
        "buy": "0.00001191",
        "sell": "0.00001206",
        "changeRate": "0.057",
        "changePrice": "0.00000065",
        "high": "0.0000123",
        "low": "0.00001109",
        "vol": "45161.5073",
        "volValue": "2127.28693026”, 
        "last": "0.00001204"
      },
      {
        "symbol": "BCD-BTC",
        "symbolName": "BCD-BTC",
        "buy": "0.00018564",
        "sell": "0.0002",
        "changeRate": "-0.0753",
        "changePrice": "-0.00001522",
        "high": "0.00021489",
        "low": "0.00018351",
        "vol": "72.99679763",
        "volValue": "2127.28693026”, 
        "last": "0.00018664"
      }
    ]
  }
```

Request market tickers for all the trading pairs in the market (including 24h volume).

On the rare occasion that we will change the currency name, if you still want the changed symbol name, you can use the symbolName field instead of the symbol field via “Get all tickers” endpoint.

###HTTP REQUEST
**GET /api/v1/market/allTickers**


### RESPONSES
Field |  Description
--------- | -----------
symbol |  Symbol
symbolName | Name of trading pairs, it would change after renaming
buy |   Best bid price
sell |  Best ask price
changeRate |  Change rate
changePrice | Change price
high |  Highest price
low |  Lowest price
vol |  The executed number in base currency
volValue | The executed amount in quote currency
last |  The last traded price

<aside class="spacer8"></aside>

## Get 24hr Stats

```json
//Get 24hr Stats
{
    "symbol": "ETH-BTC",    // symbol
    "high": "0.03736329",   // 24h highest price
    "vol": "2127.286930263025",  // 24h volume，the aggregated trading volume in ETH
    "volValue": "43.58567564",  // 24h total, the trading volume in quote currency of last 24 hours
    "last": "0.03713983",   // last price
    "low": "0.03651252",    // 24h lowest price
    "buy": "0.03712118",    // bestAsk
    "sell": "0.03713983",   // bestBid
    "changePrice": "0.00037224",  // 24h change price
    "averagePrice": "8699.24180977",//24h average transaction price yesterday
    "time": 1550847784668,  //time
    "changeRate": "0.0101" // 24h change rate
}
```  

Request via this endpoint to get the statistics of the specified ticker in the last 24 hours.

###HTTP REQUEST
**GET /api/v1/market/stats**

### Example
GET /api/v1/market/stats?symbol=BTC-USDT

###PARAMETERS

Param | Type | Description
--------- | ------- | -----------
symbol | String | [symbol](#get-symbols-list)


### RESPONSES
Field |  Description
--------- | -----------
symbol | Symbol
high | Highest price in 24h
vol | 24h volume, executed based on base currency
volValue | 24h traded amount
last | Last traded price
low |  Lowest price in 24h
buy |  Best bid price
sell | Best ask price
changeRate |  24h change rate
averagePrice | Avergage trading price in the last 24 hours
changePrice | 24h change price
time |  timestamp

<aside class="spacer2"></aside>

## Get Market List

```json
//Get Market List
{
	"data":[
    "BTC",
    "KCS",
    "USDS",  //SC has been changed to USDS
    "ALTS" //ALTS market includes ETH, NEO, TRX
  ]
}
```  

Request via this endpoint to get the transaction currency for the entire trading market.

<aside class="notice">SC has been changed to USDS, but you can still use SC as a query parameter</aside>
<aside class="notice">The three markets of ETH, NEO and TRX are merged into the ALTS market. You can query the trading pairs of the ETH, NEO and TRX markets through the ALTS trading area.</aside>

###HTTP REQUEST
**GET /api/v1/markets**

### Example
GET /api/v1/markets


<aside class="spacer2"></aside>

# Order Book

## Get Part Order Book(aggregated)

```json
{
    "sequence": "3262786978",
    "time": 1550653727731,
    "bids": [["6500.12", "0.45054140"],
             ["6500.11", "0.45054140"]],  //[price，size]
    "asks": [["6500.16", "0.57753524"],
             ["6500.15", "0.57753524"]]   
}
```

Request via this endpoint to get a list of open orders for a symbol.

Level-2 order book includes all bids and asks (aggregated by price), this level returns only one size for each active price (as if there was only a single order for that price).

Query via this endpoint and the system will return only part of the order book to you. If you request level2_20, the system will return you 20 pieces of data (ask and bid data) on the order book. If you request level_100, the system will return 100 pieces of data (ask and bid data) on the order book to you. You are recommended to request via this endpoint as the system reponse would be faster and cosume less traffic.


To maintain up-to-date Order Book, please use [Websocket](#level-2-market-data) incremental feed after retrieving the Level 2 snapshot.



###HTTP REQUEST

**GET /api/v1/market/orderbook/level2_20**

**GET /api/v1/market/orderbook/level2_100**

### Example 
GET /api/v1/market/orderbook/level2_20?symbol=BTC-USDT
GET /api/v1/market/orderbook/level2_100?symbol=BTC-USDT

###PARAMETERS

Param | Type | Description
--------- | ------- | -----------
symbol | String | [symbol](#get-symbols-list)

### RESPONSES

Field |  Description
--------- | -----------
sequence | Sequence number
time | Timestamp
bids | bids
asks | asks

### Data Sort

**Asks**: Sort price from low to high

**Bids**: Sort price from high to low



## Get Full Order Book(aggregated)

```json
{
    "sequence": "3262786978",
    "time": 1550653727731,
    "bids": [["6500.12", "0.45054140"],
             ["6500.11", "0.45054140"]],  //[price，size]
    "asks": [["6500.16", "0.57753524"],
             ["6500.15", "0.57753524"]]  
}
```

Request via this endpoint to get the order book of the specified symbol.

Level 2 order book includes all bids and asks (aggregated by price). This level returns only one aggregated size for each price (as if there was only one single order for that price).

This API will return data with **full** depth.

It is generally used by professional traders because it uses more server resources and traffic, and we have strict access frequency control.

To maintain up-to-date Order Book, please use [Websocket](#level-2-market-data) incremental feed after retrieving the Level 2 snapshot.


###HTTP REQUEST

**GET /api/v1/market/orderbook/level2**  (Will be deprecated on December 31, 2019)

**GET /api/v2/market/orderbook/level2**  (Recommend)

### Example
GET /api/v1/market/orderbook/level2?symbol=BTC-USDT
GET /api/v2/market/orderbook/level2?symbol=BTC-USDT

###PARAMETERS

Param | Type | Description
--------- | ------- | -----------
symbol | String | [symbol](#get-symbols-list)

### RESPONSES

Field |  Description
--------- | -----------
sequence | Sequence number
time | Timestamp
bids | bids
asks | asks

### Data Sort ###

**Asks**: Sort price from low to high (v2)

**Asks**: Sort price from high to low (v1)

**Bids**: Sort price from high to low (v1 & v2)


## Get Full Order Book(atomic)


```json
 {
        "sequence": "1545896707028",
        "time": 1550653727731,
        "bids": [
            [
                "5c2477e503aa671a745c4057",           //orderId
                "6",                                  //price
                "0.999"                               //size
            ],
            [
                "5c2477e103aa671a745c4054",
                "5",
                "0.999"
            ]
        ],
        "asks": [
            [
                "5c24736703aa671a745c401e",           
                "200",                               
                "1"                                 
            ],
            [
                "5c2475c903aa671a745c4033",
                "201",
                "1"
            ]
        ]
    }
```
Request via this endpoint to get the Level 3 order book of the specified trading pari. Level 3 order book includes all bids and asks (the data is non-aggregated, and each item means a single order).
 

This API is generally used by professional traders because it uses more server resources and traffic, and we have strict access frequency control.

To maintain up-to-date order book, please use [Websocket](#full-matchengine-data-level-3) incremental feed after retrieving the Level 3 snapshot.

In the orderbook, the selling data is sorted low to high by price and orders with the same price are sorted in time sequence. The buying data is sorted high to low by price and orders with the same price are sorted in time sequence. The matching engine will match the orders according to the price and time sequence.


###HTTP REQUEST
**GET /api/v1/market/orderbook/level3**

### Example
GET /api/v1/market/orderbook/level3?symbol=BTC-USDT

###PARAMETERS

Param | Type | Description
--------- | ------- | -----------
symbol | String | [symbol](#get-symbols-list)

### RESPONSES

Field |  Description
--------- | -----------
sequence | Sequence number
time | Timestamp
bids | bids
asks | asks

### Data Sort 

**Asks**: Sort price from low to high

**Bids**: Sort price from high to low

<aside class="spacer4"></aside>

# Histories

## Get Trade Histories

```json
[
  {
      "sequence": "1545896668571",
      "price": "0.07",                      //Filled price
      "size": "0.004",                      //Filled amount
      "side": "buy",                        //Filled side. The filled side is set to the taker by default.
      "time": 1545904567062140823           //Transaction time
  },
  {
      "sequence": "1545896668578",
      "price": "0.054",
      "size": "0.066",
      "side": "buy",
      "time": 1545904581619888405
  }
]
```
Request via this endpoint to get the trade history of the specified symbol.


###HTTP REQUEST
**GET /api/v1/market/histories**

### Example
GET /api/v1/market/histories?symbol=BTC-USDT

###PARAMETERS

Param | Type | Description
--------- | ------- | -----------
symbol | String | [symbol](#get-symbols-list)

### RESPONSES

Field |  Description
--------- | -----------
sequence | Sequence number
time | Transaction time
price | Filled price
size |  Filled amount
side | Filled side. The filled side is set to the taker by default


###SIDE
The trade side indicates the taker order side. A taker order is the order that was matched with orders opened on the order book.

<aside class="spacer2"></aside>

## Get Klines

```json
[
  [
      "1545904980",             //Start time of the candle cycle
      "0.058",                  //opening price
      "0.049",                  //closing price
      "0.058",                  //highest price
      "0.049",                  //lowest price
      "0.018",                  //Transaction amount
      "0.000945"                //Transaction volume
  ],
  [
      "1545904920",
      "0.058",
      "0.072",
      "0.072",
      "0.058",
      "0.103",
      "0.006986"
  ]
]
```
Request via this endpoint to get the kline of the specified symbol. Data are returned in grouped buckets based on requested type.


<aside class="notice"> Klines data may be incomplete. No data is published for intervals where there are no ticks.</aside>

<aside class="warning"> Klines should not be polled frequently. If you need real-time information, use the trade and book endpoints along with the websocket feed.</aside>

###HTTP REQUEST
**GET /api/v1/market/candles**

### Example
GET /api/v1/market/candles?type=1min&symbol=BTC-USDT&startAt=1566703297&endAt=1566789757

Param | Type | Description
--------- | ------- | -----------
symbol | String | [symbol](#get-symbols-list)
startAt| long | *[Optional]*  Start time (milisecond), default is 0
endAt| long | *[Optional]* End time (milisecond), default is 0
type | String |Type of candlestick patterns: **1min, 3min, 5min, 15min, 30min, 1hour, 2hour, 4hour, 6hour, 8hour, 12hour, 1day, 1week**

<aside class="notice">For each query, the system would return at most **1500** pieces of data. To obtain more data, please page the data by time.</aside>

### RESPONSES 

Field |  Description
--------- | -----------
time | Start time of the candle cycle
open |  Opening price
close | Closing price
high | Highest price
low | Lowest price
volume |Transaction volume
turnover | Transaction amount



# Currencies


## Get Currencies

```json

[{
    "currency": "BTC",
    "name": "BTC",
    "fullName": "Bitcoin",
    "precision": 8,
    "withdrawalMinSize": "0.002",
    "withdrawalMinFee": "0.0005",
    "isWithdrawEnabled": true,   
    "isDepositEnabled": true
},
{

    "currency": "ETH",
    "name": "ETH",
    "fullName": "Ethereum",
    "precision": 8,
    "withdrawalMinSize": "0.02",
    "withdrawalMinFee": "0.01",
    "isWithdrawEnabled": true,
    "isDepositEnabled": true
  
}]

```

Request via this endpoint to get the currency list.

<aside class="notice">Not all currencies currently can be used for trading.</aside>


### HTTP REQUEST
**GET /api/v1/currencies**

### Example
GET /api/v1/currencies


**Response**

|field | description|
-----|-----
|currency| A unique currency code that will never change|
|name| Currency name, will change after renaming|
|fullName| Full name of a currency, will change after renaming |
|precision| Currency precision |
|withdrawalMinSize| Minimum withdrawal amount |
|withdrawalMinFee|  Minimum fees charged for withdrawal |
|isWithdrawEnabled| Support withdrawal or not |
|isDepositEnabled| Support deposit or not |

**CURRENCY CODES**

Currency codes will conform to the ISO 4217 standard where possible. Currencies which have or had no representation in ISO 4217 may use a custom code.

Code | Description
--------- | -------  
BTC | Bitcoin
ETH | Ethereum
KCS | Kucoin Shares

For a coin, the "**currency**" is a fixed value and works as the only recognized identity of the coin. As the "**name**", "**fullnane**" and "**precision**" of a coin are modifiable values, when the "**name**" of a coin is changed, you should use "**currency**" to get the coin. 

For example:

The "**currency**" of XRB is "XRB", if the "**name**" of XRB is changed into "**Nano**", you should use "XRB" (the currency of XRB) to search the coin. 

## Get Currency Detail


```json
{
    "currency": "BTC",
    "name": "BTC",
    "fullName": "Bitcoin",
    "precision": 8,
    "withdrawalMinSize": "0.002",
    "withdrawalMinFee": "0.0005",
    "isWithdrawEnabled": true,
    "isDepositEnabled": true
  }
```
Request via this endpoint to get the currency details of a specified currency

### HTTP REQUEST
**GET /api/v1/currencies/{currency}**

### Example
GET /api/v1/currencies/BTC

<aside class="notice">Details of the currency.</aside>

###PARAMETERS
Param | Type | Description
--------- | ------- | -----------
currency | String | **Path parameter**. [Currency](#get-currencies)
chain | String | *[Optional]* Support for querying the chain of currency, e.g. The available value for USDT are OMNI, ERC20, TRC20. This only apply for multi-chain currency, and there is no need for single chain currency.

**Response**

|field | description|
-----|-----
|currency| A unique currency code that will never change|
|name| Currency name, will change after renaming |
|fullName| Full name of a currency, will change after renaming |
|precision| Currency precision |
|withdrawalMinSize| Minimum withdrawal amount |
|withdrawalMinFee| Minimum fees charged for withdrawal |
|isWithdrawEnabled| Support withdrawal or not |
|isDepositEnabled| Support deposit or not |

## Get Fiat Price



```json
{
    "code": "200000",
    "data": {
        "BTC": "3911.28000000",
        "ETH": "144.55492453",
        "LTC": "48.45888179",
        "KCS": "0.45546856"
    }
}
```
Request via this endpoint to get the fiat price of the currencies for the available trading pairs.  

###HTTP REQUEST
**GET /api/v1/prices**

### Example
GET /api/v1/prices

###PARAMETERS
|field | description|
-----|-----
|base| *[Optional]* Ticker symbol of a base currency,eg.USD,EUR. Default is USD |
| currencies | *[Optional]* Comma-separated cryptocurrencies to be converted into fiat, e.g.: BTC,ETH, etc. Default to return the fiat price of all currencies.|

# Others

# Time

## Server Time

```json
{  
  "code":"200000",
  "msg":"success",
  "data":1546837113087
}
```

Get the API server time.

### HTTP REQUEST
**GET /api/v1/timestamp**

### Example
GET /api/v1/timestamp


# Websocket Feed

While there is a strict access frequency control for REST API, we highly recommend that API users utilize Websocket to get the real-time data.


<aside class="notice">The recommended way is to just create a websocket connection and subscribe to multiple channels.
</aside>

## Apply connect token

```json
{
    "code": "200000",
    "data": {
        "instanceServers": [
            {
                "pingInterval": 50000,
                "endpoint": "wss://push1-v2.kucoin.com/endpoint",
                "protocol": "websocket",
                "encrypt": true,
                "pingTimeout": 10000
            }
        ],
        "token": "vYNlCtbz4XNJ1QncwWilJnBtmmfe4geLQDUA62kKJsDChc6I4bRDQc73JfIrlFaVYIAE0Gv2--MROnLAgjVsWkcDq_MuG7qV7EktfCEIphiqnlfpQn4Ybg==.IoORVxR2LmKV7_maOR9xOg=="
    }
}
```

You need to apply for one of the two tokens below to create a websocket connection.

### Public token (No authentication required):

If you only use public channels (e.g. all public market data), please make request as follows to obtain the server list and temporary public token:

#### HTTP REQUEST

**POST /api/v1/bullet-public**

### Private channels (Authentication request required):

```json
{
    "code": "200000",
    "data": {
        "instanceServers": [
            {
                "pingInterval": 50000,
                "endpoint": "wss://push1-v2.kucoin.com/endpoint",
                "protocol": "websocket",
                "encrypt": true,
                "pingTimeout": 10000
            }
        ],
        "token": "vYNlCtbz4XNJ1QncwWilJnBtmmfe4geLQDUA62kKJsDChc6I4bRDQc73JfIrlFaVYIAE0Gv2--MROnLAgjVsWkcDq_MuG7qV7EktfCEIphiqnlfpQn4Ybg==.IoORVxR2LmKV7_maOR9xOg=="
    }
}
```

For private channels and messages (e.g. account balance notice), please make request as follows after authorization to obtain the server list and authorized token.

#### HTTP REQUEST

**POST /api/v1/bullet-private**


### Response

|Field | Description|
-----|-----
|pingInterval| Recommended to send ping interval in millisecond|
|pingTimeout| After such a long time(millisecond), if you do not receive pong, it will be considered as disconnected. |
|endpoint| Websocket server address for establishing connection|
|protocol| Protocol supported|
|encrypt| Indicate whether SSL encryption is used |
|token| token|

## Create connection

```javascript
var socket = new WebSocket("wss://push1-v2.kucoin.com/endpoint?token=xxx&[connectId=xxxxx]&acceptUserMessage=true");
```


When the connection is successfully established, the system will send a welcome message.

**connectId**: the connection id, a unique value taken from the client side. Both the id of the welcome message and the id of the error message are connectId.

**acceptUserMessage**: if the value of acceptUserMessage equal with true, the User Messages can be received.

```json
{
  "id":"hQvf8jkno",
  "type":"welcome"
}
```



<aside class="spacer2"></aside>

## Ping
```json
{
  "id":"1545910590801",
  "type":"ping"
}
```


To prevent the TCP link being disconnected by the server, the client side needs to send ping messages to the server to keep alive the link.

After the ping message is sent to the server, the system would return a pong message to the client side.

If the server has not received the ping from the client for **60 seconds** , the connection will be disconnected.

```json
{
  "id":"1545910590801",
  "type":"pong"
}
```
<aside class="spacer3"></aside>

## Subscribe

```json
{
    "id": 1545910660739,                          //The id should be an unique value
    "type": "subscribe",
    "topic": "/market/ticker:BTC-USDT,ETH-USDT",  //Topic needs to be subscribed. Some topics support to divisional subscribe the informations of multiple trading pairs through ",".
    "privateChannel": false,                      //Adopted the private channel or not. Set as false by default.
    "response": true                              //Whether the server needs to return the receipt information of this subscription or not. Set as false by default.
}
```

To subscribe channel messages from a certain server, the client side should send subscription message to the server.

If the subscription succeeds, the system will send ack messages to you, when the response is set as true.


```json
  {
    "id":"1545910660739",
    "type":"ack"
  }
```
While there are topic messages generated, the system will send the corresponding messages to the client side. For details about the message format, please check the definitions of topics.

### Parameters
#### ID
ID is unique string to mark the request which is same as id property of ack.

#### Topic
The topic you want to subscribe to.

#### PrivateChannel
For some specific topics (e.g. /market/level3), **privateChannel** is available. The default value of **privateChannel** is **False**. If the **privateChannel** is set to **true**, the user will only receive messages related himself on the topic. The format of the **topic** field in the returned data is **{topic}:privateChannel:{userId}**.

#### Response
If the response is set as ture, the system will return the ack messages after the subscription succeed.

## UnSubscribe
Unsubscribe from topics you have subscribed to.

```json
{
    "id": "1545910840805",                            //The id should be an unique value
    "type": "unsubscribe",
    "topic": "/market/ticker:BTC-USDT,ETH-USDT",      //Topic needs to be unsubscribed. Some topics support to divisional unsubscribe the informations of multiple trading pairs through ",".
    "privateChannel": false, 
    "response": true,                                  //Whether the server needs to return the receipt information of this subscription or not. Set as false by default.
}
```

```json
{
  "id": "1545910840805",
  "type": "ack"
}
```

### Parameters

#### ID
Unique string to mark the request.

#### Topic
The topic you want to subscribe.

#### PrivateChannel
For some specific **public** topics (e.g. /market/level3), **privateChannel** is available. The default value of **privateChannel** is **False**. If the **privateChannel** is set to **true**, the user will only receive messages related himself on the topic. The format of the **topic** field in the returned data is **{topic}:privateChannel:{userId}**.

#### Response
If the response is set as ture, the system would return the ack messages after the unsubscription succeed.

## Multiplex

In one physical connection, you could open different multiplex tunnels to subscribe different **topics** for different data.


For example, enter the command below to open **bt1** multiple tunnel :

 {"id": "1Jpg30DEdU", "type": "openTunnel", "newTunnelId": "bt1", "response": true}

Add “**tunnelId**” in the command: 

{"id": "1JpoPamgFM", "type": "subscribe", "topic": "/market/ticker:KCS-BTC"，"tunnelId": "bt1", "response": true}

You would then, receive messages corresponding to the id **tunnelIId**:  

{"id": "1JpoPamgFM", "type": "message", "topic": "/market/ticker:KCS-BTC", "subject": "trade.ticker", "tunnelId": "bt1", "data": {...}}

To close the **tunnel**, you can enter the command below: 

{"id": "1JpsAHsxKS", "type": "closeTunnel", "tunnelId": "bt1", "response": true}

##### Limitations

1. The multiplex **tunnel** is provided for API users only. 
2. The maximum multiplex tunnels available: **5**.


## Sequence Numbers
The sequence field exists in order book, trade history and snapshot messages by default and the Level 3 and Level 2 data works to ensure the full connection of the sequence. If the sequence is non-sequential, please enable the calibration logic.


## General Logic for Message Judgement in Client Side
1.Judge message type. There are three types of messages at present: message (the commonly used messages for push), notice (the notices generally used), and command (consecutive command).

2.Judge messages by userId. Messages with userId are private messages, messages without userId are common messages.

3.Judge messages by topic. You could judge the message type through the topic. 

4.Judge messages by subject. For the same type of messages with the same topic, you could judge the type of messages through their subjects. 

# Public Channels

## Symbol Ticker 

```json

{
    "id": 1545910660739,                          
    "type": "subscribe",
    "topic": "/market/ticker:BTC-USDT",
    "response": true                              
}
```
Topic: **/market/ticker:{symbol},{symbol}...**

```json
{
  "type":"message",
  "topic":"/market/ticker:BTC-USDT",
  "subject":"trade.ticker",
  "data":{
    "sequence":"1545896668986", // Sequence number
    "bestAsk":"0.08",  // Best ask price
    "size":"0.011",   //  Last traded amount
    "bestBidSize":"0.036",  // Best bid size
    "price":"0.08",  // Last traded price
    "bestAskSize":"0.18",  // Best ask size
    "bestBid":"0.049" // Best bid price
  }
}
```
Subscribe to this topic to get the realtime push of BBO changes.

The ticker channel provides real-time price updates whenever a match happens. If multiple orders are matched at the same time, only the last matching event will be pushed.


Please note that more information maybe added to messages from this channel in the near future.


<aside class="spacer2"></aside> 
<aside class="spacer4"></aside> 


## All Symbols Ticker

```json

{
    "id": 1545910660739,                          
    "type": "subscribe",
    "topic": "/market/ticker:all",
    "response": true                              
}
```
Topic: **/market/ticker:all**

```json
{
  "type":"message",
  "topic":"/market/ticker:all",
  "subject":"BTC-USDT",
  "data":{
    "sequence":"1545896668986",
    "bestAsk":"0.08",
    "size":"0.011",
    "bestBidSize":"0.036",
    "price":"0.08",
    "bestAskSize":"0.18",
    "bestBid":"0.049"
  }
}
```
Subscribe to this topic to get the real time push of all market symbols BBO change.


<aside class="spacer2"></aside> 
<aside class="spacer4"></aside> 


## Symbol Snapshot

```json
{
	"data": {
		"sequence": "1545896669291",
		"data": [{
			"trading": true,
			"symbol": "KCS-BTC",
			"buy": 0.00011,
			"sell": 0.00012,
			"sort": 100,
			"volValue": 3.13851792584,
			"baseCurrency": "KCS",
			"market": "BTC",
			"quoteCurrency": "BTC",
			"symbolCode": "KCS-BTC",
			"datetime": 1548388122031,
			"high": 0.00013,
			"vol": 27514.34842,
			"low": 0.0001,
			"changePrice": -1.0e-5,
			"changeRate": -0.0769,
			"lastTradedPrice": 0.00012,
			"board": 0,
			"mark": 0
		}]
	},
	"subject": "trade.snapshot",
	"topic": "/market/snapshot:BTC",
	"type": "message"
}
```

Topic: **/market/snapshot:{symbol}**

Subscribe to get snapshot data for a single symbol.

The snapshot data is pushed at **2 seconds** intervals.

<aside class="spacer4"></aside> 
<aside class="spacer4"></aside> 
<aside class="spacer"></aside> 

## Market Snapshot

```json
{
	"data": {
		"sequence": "1545896669291",
		"data": {
			"trading": true,
			"symbol": "KCS-BTC",
			"buy": 0.00011,
			"sell": 0.00012,
			"sort": 100,
			"volValue": 3.13851792584,   //total
			"baseCurrency": "KCS",
			"market": "BTC",
			"quoteCurrency": "BTC",
			"symbolCode": "KCS-BTC",
			"datetime": 1548388122031,
			"high": 0.00013,
			"vol": 27514.34842,
			"low": 0.0001,
			"changePrice": -1.0e-5,
			"changeRate": -0.0769,
			"lastTradedPrice": 0.00012,
			"board": 0,
			"mark": 0
		}
	},
	"subject": "trade.snapshot",
	"topic": "/market/snapshot:KCS-BTC",
	"type": "message"
}
```

Topic: **/market/snapshot:{market}**

Subscribe this topic to get the snapshot data of for the entire [market](#get-market-list).


The snapshot data is pushed at **2 seconds** intervals.

<aside class="spacer4"></aside> 
<aside class="spacer4"></aside> 
<aside class="spacer"></aside> 

## Level-2 Market Data

```json
{
    "id": 1545910660740,                          
    "type": "subscribe",
    "topic": "/market/level2:BTC-USDT",
    "response": true                              
}
```

Topic: **/market/level2:{symbol},{symbol}...**

Subscribe to this topic to get Level2 order book data.

When the websocket subscription is successful,  the system would send the increment change data pushed by the websocket to you.

```json
{
  "type":"message",
  "topic":"/market/level2:BTC-USDT",
  "subject":"trade.l2update",
  "data":{
    "sequenceStart":1545896669105,
    "sequenceEnd":1545896669106,
    "symbol":"BTC-USDT",
    "changes":{
      "asks":[["6","1","1545896669105"]],           //price, size, sequence
      "bids":[["4","1","1545896669106"]]
    }
  }
}
```

Calibration procedure：

1. After receiving the websocket Level 2 data flow, cache the data.
2. Initiate a [REST](#get-full-order-book-aggregated) request to get the snapshot data of Level 2 order book.
3. Playback the cached Level 2 data flow.
4. Apply the new Level 2 data flow to the local snapshot to ensure that the sequence of the new Level 2 update lines up with the sequence of the previous Level 2 data. Discard all the message prior to that sequence, and then playback the change to snapshot.
5. Update the level2 full data based on sequence according to the size. If the price is 0, ignore the messages and update the sequence. If the size=0, update the sequence and remove the price of which the size is 0 out of level 2. For other cases, please update the price.


**Example**

Take BTC/USDT as an example, suppose the current order book data in level 2 is as follows:

After subscribing to the channel, you would receive changes as follows:

"asks":[

  ["3988.62","8", 15],

  ["3988.61","0", 18],

  ["3988.59","3", 16],

]

"bids":[

  ["3988.50", "44", "17"]

]

<aside class="notice">Description: the message format is [Price, Size, Sequence].</aside>

Get a snapshot of the order book through a **REST** request ([Get Order Book](#get-part-order-book-aggregated)) to build a local order book. Suppose that data we got is as follows:

Sequence：**16**

Data：

"asks":[

  ["3988.62","8"],

  ["3988.61","32"],

  ["3988.60","47"],

  ["3988.59","3"],

]

"bids":[

  ["3988.51","56"],

  ["3988.50","15"],

  ["3988.49","100"],

  ["3988.48","10"]

]

The current data on the local order book is as follows:

| Price   | Size | Side |
| ------- | ---- | ---- |
| 3988.62 | 8    | Sell |
| 3988.61 | 32   | Sell |
| 3988.60 | 47   | Sell |
| 3988.59 | 3    | Sell |
| 3988.51 | 56   | Buy  |
| 3988.50 | 15   | Buy  |
| 3988.49 | 100  | Buy  |
| 3988.48 | 10  | Buy  |

In the beginning, the sequence of the order book is 16. Discard the feed data of sequence that is below or equals to 16, and apply playback the sequence [17,18] to update the snapshot of the order book. Now the sequence of your order book is 18 and your local order book is up-to-date.

**Diff:**

1.**Update size of 3988.50 to 44 (Sequence 17)**

2.**Remove 3988.61 (Sequence 18)**

Now your current order book is up-to-date and final data is as follows:

| Price   | Size | Side |
| ------- | ---- | ---- |
| 3988.62 | 8    | Sell |
| 3988.60 | 47   | Sell |
| 3988.59 | 3    | Sell |
| 3988.51 | 56   | Buy  |
| 3988.50 | 44   | Buy  |
| 3988.49 | 100  | Buy  |
| 3988.48 | 10  | Buy  |

## Match Execution Data

```json
{
    "id": 1545910660741,                          
    "type": "subscribe",
    "topic": "/market/match:BTC-USDT",
    "privateChannel": false,                      
    "response": true                              
}
```
Topic: **/market/match:{symbol},{symbol}...**

For this topic, **privateChannel** is available.

Subscribe to this topic to obtain the matching event data flow of Level 3.

For each order traded, the system would send you the match messages in the following format.

```json
{
  "id":"5c24c5da03aa673885cd67aa",
  "type":"message",
  "topic":"/market/match:BTC-USDT",
  "subject":"trade.l3match",
  "data":{
    "sequence":"1545896669145",
    "symbol":"BTC-USDT",
    "side":"buy",
    "size":"0.01022222000000000000",
    "price":"0.08200000000000000000",
    "takerOrderId":"5c24c5d903aa6772d55b371e",
    "time":"1545913818099033203",
    "type":"match",
    "makerOrderId":"5c2187d003aa677bd09d5c93",
    "tradeId":"5c24c5da03aa673885cd67aa"
  }
}
```
<aside class="spacer8"></aside>
<aside class="spacer"></aside>

## Full MatchEngine Data(Level 3)

```json
{
    "id": 1545910660742,                          
    "type": "subscribe",
    "topic": "/market/level3:BTC-USDT",
    "privateChannel": false,                      
    "response": true                              
}
```

Topic: **/market/level3:{symbol},{symbol}...**

For this topic, **privateChannel** is available.

Subscribe this topic to get the updated data for orders and trades.

This channel provides real-time updates on orders and trades. These updates can be applied on to a Level 3 order book snapshot for users to maintain an accurate and up-to-date copy of the exchange order book.

<aside class="notice">Note: If you are maintaining a Level 2 order book, please switch to the Level 2 channel.
</aside>

The process to maintain an up-to-date Level 3 order book is described below.

1. Send a subscribe message for a symbol of which you want to build the order book.
2. Queue every messages received over the websocket stream.
3. Make a [REST](#get-full-order-bookatomic) request to get the snapshot data of the order book.
4. Playback queued messages, and discard sequence numbers before or equal to the snapshot sequence number.
5. Apply playback messages to the snapshot as needed (see below).
6. After playback is complete, apply real-time stream messages as they arrive.


###MESSAGE TYPE

The following messages(**RECEIVED, OPEN, UPDATE, MATCH, DONE**) are sent over the websocket stream in JSON format after subscribing to this channel:


###RECEIVED

```json
{
	"type": "message",
	"topic": "/market/level3:BTC-USDT",
	"subject": "trade.l3received",
	"data": {
		"sequence": "1545896669147",
		"symbol": "BTC-USDT",
		"side": "sell",  //side, include buy and sell
		"orderId": "5c24c72503aa6772d55b378d",  //order id
		"price": "4.00000000000000000000", 
		"time": "1545914149935808589",  //timestamp, timestamps is nanosecond
		"clientOid": "",   //unique order id is selected by you to identify your order, e.g. UUID
		"type": "received",  //L3 messege type. If it is a received message, the update is ended.		
		"orderType": "limit" // order type,e.g. limit,market,stop_limit
	}
}
```

```json
{
	"type": "message",
	"topic": "/market/level3:BTC-USDT",
	"subject": "trade.l3received",
	"data": {
		"sequence": "1545896669100",
		"symbol": "BTC-USDT",
		"side": "sell",
		"orderId": "5c24c72503aa6772d55b178d",
		"time": "1545914149835808589",
		"clientOid": "",
		"type": "received",
		"orderType": "market"
	}
}
```

When the matching engine receives an order command, the system would send a confirmation message to the user.

This will mean that a valid order has been received and is now with an active status. This message is emitted for every single valid order as soon as the matching engine receives it whether it fills immediately or not.

The received message does not indicate a resting order on the orderbook. It simply indicates a new incoming order which has been accepted by the matching engine for processing. Received orders may cause match messages to follow if they are being filled immediately (i.e if you made a ‘taker’ order). Self-trade prevention may also trigger change messages to follow if the order size needs to be adjusted. Orders which are not fully filled or canceled due to self-trade prevention result in an open message and become resting orders on the orderbook.

<aside class="notice">You can filter your orders through clientOid, but it will be posted to L3 message (it may cause your orders strategy to be known for others), it is recommended that you can use UUID as clientOid.
</aside>

<aside class="spacer8"></aside>
<aside class="spacer4"></aside>


###OPEN

```json
{
  "type":"message",
  "topic":"/market/level3:BTC-USDT",
  "subject":"trade.l3open",
  "data":{
    "sequence":"1545896669148",
    "symbol":"BTC-USDT",
    "side":"sell",  //side, include buy and sell
    "size":"1", //order quantity
    "orderId":"5c24c72503aa6772d55b378d",  //order id
    "price":"6.00000000000000000000",
    "time":"1545914149935808632", //timestamp, timestamps is nanosecond
    "type":"open"  //L3 messege type. If it is an open message, add the corresponding buy or sell order built by orderid, price and size
  }
}
```

When the remaining part in a limit order enters the order book, the system will send an open message to the user.

This will mean that the order is now open on the order book. This message will only be sent for orders which are not fully filled immediately. remaining_size will indicate how much of the order is unfilled and going on the book.

<aside class="notice">When price="" is received, size="0" is hidden.</aside>

<aside class="spacer4"></aside>
<aside class="spacer"></aside>

###DONE

When the matching life cycle of an order ends, the order will no longer be displayed on the order book and the system will send a done message to the user.

```json
{
  "type":"message",
  "topic":"/market/level3:BTC-USDT",
  "subject":"trade.l3done",
  "data":{
    "sequence":"1545896669226",
    "symbol":"BTC-USDT",
    "reason":"filled",
    "side":"buy",
    "orderId":"5c24c96103aa6772d55b380b",
    "time":"1545914730696727106",
    "type":"done"
  }
}
```

```json
{
  "type":"message",
  "topic":"/market/level3:BTC-USDT",
  "subject":"trade.l3done",
  "data":{
    "sequence":"1545896669227",
    "symbol":"BTC-USDT",
    "reason":"canceled",  //Order completion status, include canceled and filled
    "side":"buy",  //side, include buy and sell
    "orderId":"5c24c96103aa6772d55b381b",  //order id
    "time":"1545914730696797106",  //timestamp, timestamps is nanosecond
    "type":"done", //L3 messege type. If it is a done message, remove the buy or sell order corresponding to the orderid
    "size": "1.12340000000000000000"  //order quantity
  }
}
```

This will mean that the order is no longer on the order book. The message is sent for all orders for which there was a received message. This message can result from an order being canceled or filled. There will be no more messages for this order_id after a done message. remain_size indicates how much of the order went unfilled; this will be 0 for filled orders.

market orders will not have a remaining_size or price field as they are never on the open order book at a given price.

<aside class="spacer8"></aside>
<aside class="spacer3"></aside>

###MATCH

```json
{
  "type":"message",
  "topic":"/market/level3:BTC-USDT",
  "subject":"trade.l3match",
  "data":{
    "sequence":"1545896669291",
    "symbol":"BTC-USDT",
    "side":"buy",  //side, include buy and sell
    "size":"0.07600000000000000000",  //order quantity
    "price":"0.08300000000000000000",  
    "takerOrderId":"5c24ca2e03aa6772d55b38bf",  //Extract liquidity user order id
    "time":"1545914933083576866",  //timestamp, timestamps is nanosecond
    "type":"match",  //L3 messege type. If it is a match message, reduce the number of order corresponding to the markerOrderId
    "makerOrderId":"5c20492a03aa677bd099ce9d",  //Provide liquidity user order id
    "tradeId":"5c24ca3503aa673885cd67ef"  //match_id，a match to generate two orderids when orders were matched
  }
}
```
When two orders become matched, the system will send a match message to user.

The match message indicates that a trade occurred between two orders. The aggressor or taker order is the one executing immediately after being received and the maker order is a resting order on the book. The side field indicates the maker order side. If the side is sell this indicates the maker was a sell order and the match is considered an up-tick. Respectively, a buy side match is a down-tick.

<aside class="notice">Before entering the orderbook, the iceberg or hidden order is the same as the ordinary order when it is matched as taker(it has a takerOrderId).</aside>

<aside class="spacer4"></aside>
<aside class="spacer2"></aside>

###CHANGE###

```json
{
  "type":"message",
  "topic":"/market/level3:BTC-USDT",
  "subject":"trade.l3change",
  "data":{
    "sequence":"1545896669656",
    "symbol":"BTC-USDT",
    "side":"buy",  //side, include buy and sell
    "orderId":"5c24caff03aa671aef3ca170",  //order id
    "price":"1.00000000000000000000",
    "newSize":"0.15722222000000000000",  //Updated order quantity
    "time":"1545915145402532254",  //timestamp, timestamps is nanosecond
    "type":"change",  //L3 messege type. If it is a change message, modify the number of buy or sell order corresponding to the orderid
    "oldSize":"0.18622222000000000000"  //order quantity before update
  }
}
```

When an order is changed due to STP, the system would send a change message to the user.
This is the result of self-trade prevention adjusting the order size or available funds. Orders can only decrease in size or funds. Change messages are always sent when an order changes in size; this includes resting orders (open) as well as received but not yet open orders. Change messages are also sent when a new market order goes through self trade prevention and the funds for the market order have changed.

<aside class="spacer8"></aside>
<aside class="spacer4"></aside>

### How to manage a local L3 orderbook correctly###

1.Use the websocket channel: **/market/level3:{symbol}** to subscribe to the level3 incremental data and cache all incremental data received.

2.Get the snapshot data of level3 through the rest interface **https://api.kucoin.com/api/v1/market/orderbook/level3?symbol={symbol}**.

3.Verify the data that you received. The sequence of the snapshot should not  be less than the minimum sequence of all increments of the cache. If this condition is not met, start from the first step.

4.Playback all cached incremental data:

4.1 If the sequence of the incremental data is less or equal to the sequence of the current snapshot, discard the incremental data and end the update; otherwise proceed to 4.2.

4.2 If the sequence of incremental data = sequence+1 of the current snapshot, proceed to 4.2.1 logical update, otherwise proceed to step 4.3.

4.2.1 Update the sequence of the current snapshot to the sequence of the incremental data.

4.2.2 If it is a received message, end the update logic. (because now the received message does not affect the level3 data).

4.2.3 If it is an open message, add the corresponding buy or sell order built by orderid, price and size.

4.2.4 If it is a done message, remove the buy or sell order corresponding to the orderid.

4.2.5 If it is a change message, modify the number of buy or sell order corresponding to the orderid.

4.2.6 If it is a match message, reduce the number of order corresponding to the markerOrderId.

4.3 In this case, the sequence is not continuous. Perform step 2 and re-pull the snapshot data to ensure that the sequence is not missing.

5.Receive the new incremental data push and go to step 4.

When you maintain a local L3 orderbook data, if you can't fully understand the following examples, we provide a L3 orderbook maintenance case based on the Go language which you can refer to. This example mainly includes how to update the L3 data under different events, well-maintained orderbook, the data format of the websocket message and so on. The specific link is as follows: [L3 demo](https://github.com/Kucoin/kucoin-go-level3-demo)

<aside class="spacer4"></aside>
<aside class="spacer2"></aside>

# Private Channels

Subscribe to private channels require **privateChannel=“true”**.

## Stop order received event

```json
{
  "type":"message",
  "topic":"/market/level3:BTC-USDT",
  "subject":"trade.l3received",
  "data": {
    "sequence":"1545738118241",
    "symbol":"BTC-USDT",
    "side":"buy",
    "orderId":"5c21e80303aa677bd09d7dff",
    "stopType":"entry",
    "funds":"1.00000000000000000000",
    "time":"1545743136994328401",
    "type":"stop"
  }
}
```
Topic: **/market/level3:{symbol},{symbol}...**

When a stop-limit order is received by the system, you will receive a stop message which means that this order entered the stop queue and waited to be triggered.

<aside class="spacer4"></aside>
<aside class="spacer"></aside>

##Stop order activate event

```json
{
  "type":"message",
  "topic":"/market/level3:BTC-USDT",
  "subject":"trade.l3received",
  "data": {
    "sequence":"1545738118241",
    "symbol":"BTC-USDT",
    "side":"buy",
    "orderId":"5c21e80303aa677bd09d7dff",
    "stopType":"entry",
    "funds":"1.00000000000000000000",
    "time":"1545743136994328401",
    "type":"activate"
  }
}
```
Topic: **/market/level3:{symbol},{symbol}...**

When a stop-limit order is triggered, you will receive an activate message which means that this order started the matching life cycle.

<aside class="spacer4"></aside>
<aside class="spacer"></aside>

## Account balance notice
```json
{
	"type": "message",
	"topic": "/account/balance",
	"subject": "account.balance",
	"data": {
		"total": "88",
		"available": "88",
		"availableChange": "88",
		"currency": "KCS",
		"hold": "0",
		"holdChange": "0",
		"relationEvent": "main.deposit",
		"relationEventId": "5c21e80303aa677bd09d7dff",
		"time": "1545743136994",
		"accountId": "5bd6e9286d99522a52e458de"
	}
}

```
Topic: **/account/balance**

You will receive this message when an account balance changes. The message contains the details of the change.

<aside class="notice">You can monitor assets change through accountId.</aside>
