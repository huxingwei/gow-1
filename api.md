**GOW RESTful API**




# API Overview

Welcome to the GOW API！ You can use this API to obtain market data, perform transactions, as well as manage your account.


# Integration Overview

## Integration url

**REST API**:http://47.75.162.18:56666/

## Request Header Parameters

Request headers must include below:

* content-type：application/json
* timestamp：request timestamp, by milliseconds
* apiKey：API KEY
* sign：signature


## Signature Verificiation

### Create API KEY

API Key should include below two sections
* API KEY 
* Secret Key (for encryption, and only viewable during application)

### Signature Steps

Signature uses HmacSHA512 encryption，signature content and parameters should be linked using the "&" symbol

#### Signature Content

**GET Request**:Need to utilize apiKey and timestamp, using reverse order basis ASCII, eg
* timestamp=1566322200000&apiKey=4565B83XXXXXXXXXXXXF123

**POST Request**:Need to utilize apiKey and timestamp, using reverse order basis ASCII, eg Cancel Order:
* timestamp=1566322200000&orderId=E12345XXXXXXXX&apiKey=4565B83XXXXXXXXXXXXF123

#### Signature

Create the signature using secretKey and HmacSHA512 encryption

```java
            String timestamp = "1566322200000";
            String secretKey = "XXXXXXXXXXXXXXXXXXXXXXX";
            Mac hmacSha512 = Mac.getInstance("HmacSHA512");
            SecretKeySpec secKey = new SecretKeySpec(secretKey.getBytes(StandardCharsets.UTF_8), "HmacSHA512");
            hmacSha512.init(secKey);
            String paramStr = "timestamp=1566322200000&orderId=E12345XXXXXXXX&apiKey=4565B83XXXXXXXXXXXXF123";
            byte[] hash = hmacSha512.doFinal(paramStr.getBytes(StandardCharsets.UTF_8));
            String sign = Hex.encodeHexString(hash);

```

## Request Format

All API requests shoud be submitted using GET or POST formats.  For GET requests, all parameters are placed within the URL; For POST requests, all parameters are included within the body and header of the request using JSON formats
Must include: timestamp、apiKey、sign

## Return Format

| Param Name   | Param Decription           |    Type |  schema |
| ------------ | -------------------|-------|----------- |
|code| return code  |string  |  return 000000 success, all other codes are unsuccessful  |
|data| return data  |object  |    |
|description| return description  |string  |    |


# common

## Obtain Basic Currency Type


**Interface Description**:


**Interface URL**:`/openapi/v1/common/currencys`


**Request Method**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**Request Param**：
N/A at this time



**Return Example**:

```json
{
	"code": "",
	"data": [],
	"description": ""
}
```

**Return Param**:


| Param Name         | Param Desc                             | Type |  schema |
| ------------ | -------------------|-------|----------- |
|code| return code  |string  |    |
|data| currency type list  |array  |    |
|description| return description  |string  |    |






## Obtain Trading Pair Details


**Interace Description**:


**Interface URL**:`/openapi/v1/common/symbolInfo`


**Request Method**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**Request Param**：

| Param Name         | Param Desc     |     in |  Mandatory      |  Data Type  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|symbol| trading pair  | query | true |string  |    |

**Return Example**:

```json
{
	"code": "",
	"data": {
		"baseCoinScale": 0,
		"baseSymbol": "",
		"buyPriceLimit": 0,
		"coinScale": 0,
		"coinSymbol": "",
		"enable": 0,
		"enableMarketBuy": "",
		"enableMarketSell": "",
		"fee": 0,
		"flag": 0,
		"maxTradingOrder": 0,
		"maxTradingTime": 0,
		"maxVolume": 0,
		"minSellPrice": 0,
		"minTurnover": 0,
		"minVolume": 0,
		"sellPriceLimit": 0,
		"sort": 0,
		"symbol": "",
		"zone": 0
	},
	"description": ""
}
```

**Return Param**:


| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
|code| return code  |string  |    |
|data| return data  |ExchangeCoin  | ExchangeCoin   |
|description| return description  |string  |    |



**schema property**




**ExchangeCoin**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
|baseCoinScale | base coin decimal places   |integer(int32)  |    |
|baseSymbol | base coin symbol   |string  |    |
|buyPriceLimit | buy price limit   |number  |    |
|coinScale | traded coin decimal places   |integer(int32)  |    |
|coinSymbol | traded coin symbol   |string  |    |
|enable | status，1：enable，2：disable   |integer(int32)  |    |
|enableMarketBuy | enable market buy,value:0,1   |string  |    |
|enableMarketSell | enable market sell,value:0,1   |string  |    |
|fee | transaction fee   |number  |    |
|flag | tag，for referrals, sorting etc, default 0，1 as referral   |integer(int32)  |    |
|maxTradingOrder | maximum concurrent trade orders，0 as no limit   |integer(int32)  |    |
|maxTradingTime | maximum trading time   |integer(int32)  |    |
|maxVolume | maximum order volume，0 as no limit   |number  |    |
|minSellPrice | minimum sell price   |number  |    |
|minTurnover | minimum turnover   |number  |    |
|minVolume | minimum order volume，0 as no limit   |number  |    |
|sellPriceLimit | sell price limit   |number  |    |
|sort | sort order   |integer(int32)  |    |
|symbol | trading pair   |string  |    |
|zone | trading zone   |integer(int32)  |    |



## Request Supported Trading Pair


**Interface Description**:


**Interface URL**:`/openapi/v1/common/symbols`


**Request Method**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**Request Param**：
N/A at this time



**Request Example**:

```json
{
	"code": "",
	"data": [
		{
			"baseCoinScale": 0,
			"baseSymbol": "",
			"buyPriceLimit": 0,
			"coinScale": 0,
			"coinSymbol": "",
			"enable": 0,
			"enableMarketBuy": "",
			"enableMarketSell": "",
			"fee": 0,
			"flag": 0,
			"maxTradingOrder": 0,
			"maxTradingTime": 0,
			"maxVolume": 0,
			"minSellPrice": 0,
			"minTurnover": 0,
			"minVolume": 0,
			"sellPriceLimit": 0,
			"sort": 0,
			"symbol": "",
			"zone": 0
		}
	],
	"description": ""
}
```

**Return Param**:


| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
|code| return code  |string  |    |
|data| return data  |array  | ExchangeCoin   |
|description| return description  |string  |    |



**schema property**




**ExchangeCoin**

| Param Name         | Param Desc                             |    Type|  schema |
| ------------ | ------------------|--------|----------- |
|baseCoinScale | base coin decimal places   |integer(int32)  |    |
|baseSymbol | base coin symbol   |string  |    |
|buyPriceLimit | buy price limit   |number  |    |
|coinScale | traded coin decimal places   |integer(int32)  |    |
|coinSymbol | traded coin symbol   |string  |    |
|enable | status，1：enable，2：disable   |integer(int32)  |    |
|enableMarketBuy | enable market buy,value:0,1   |string  |    |
|enableMarketSell | enable market sell,value:0,1   |string  |    |
|fee | transaction fee   |number  |    |
|flag | tag，for referrals, sorting etc, default 0，1 as referral   |integer(int32)  |    |
|maxTradingOrder | maximum concurrent trade orders，0 as no limit   |integer(int32)  |    |
|maxTradingTime | maximum trading time   |integer(int32)  |    |
|maxVolume | maximum order volume，0 as no limit   |number  |    |
|minSellPrice | minimum sell price   |number  |    |
|minTurnover | minimum turnoer   |number  |    |
|minVolume | minimum order volume，0 as no limit   |number  |    |
|sellPriceLimit | sell price limit   |number  |    |
|sort | sort order   |integer(int32)  |    |
|symbol | trading pair   |string  |    |
|zone | trading zone   |integer(int32)  |    |


# market

## Request Order Book(Liquidity)Data


**Interface Description**:


**Interface URL**:`/openapi/v1/market/exchangePlate`


**Request Method**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**Request Param**：

| Param Name         | Param Desc     |     in |  Mandatory      |  Data Type  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|symbol| trading pair  | query | true |string  |    |

**Request Example**:

```json
{
	"code": "",
	"data": {
		"additionalProperties1": [
			{
				"amount": 0,
				"changed": true,
				"price": 0
			}
		]
	},
	"description": ""
}
```

**Return Param**:


| Return Name         | Return Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
|code| return code  |string  |    |
|data| return data  |array  | TradePlateItem   |
|description| return description  |string  |    |



**schema property**




**TradePlateItem**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
|amount | amount   |number  |    |
|changed |    |boolean  |    |
|price | price   |number  |    |

## Request Coin History K Line


**Interface Description**:


**Interface URL**:`/openapi/v1/market/history`


**Request Method**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**Request Param**：

| Param NAme         | Param Desc     |     in |  Mandatory      |  Data Type  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|from| from timestamp  | query | true |integer  |    |
|resolution| K line period(1,15,30,60,240,D,W,M)  | query | true |string  |    |
|symbol| trading pair  | query | true |string  |    |
|to| to timestampe  | query | true |integer  |    |

**Request Example**:

```json
{
	"code": "",
	"data": [],
	"description": ""
}
```

**Return Param**:


| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
|code| retun code  |string  |    |
|data| return data（sort order：timestampe, open price, high price, low price, close price, volume）  |array  |    |
|description| return desc  |string  |    |



## Request Recent Trade History


**Interface Description**:


**Interface URL**:`/openapi/v1/market/latestTrade`


**Request Method**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**Request Method**：

| Param Name         | Param Desc     |     in |  Mandatory      |  Data Type  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|size| size  | query | true |ref  |    |
|symbol| trading pair  | query | true |string  |    |

**Return Example**:

```json
{
	"code": "",
	"data": [
		{
			"amount": 0,
			"buyId": "",
			"buyOrderId": "",
			"buyTurnover": 0,
			"direction": "",
			"id": "",
			"price": 0,
			"sellId": "",
			"sellOrderId": "",
			"sellTurnover": 0,
			"symbol": "",
			"time": 0
		}
	],
	"description": ""
}
```

**Return Param**:


| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
|code| return code  |string  |    |
|data| return data  |array  | ExchangeTrade   |
|description| return description  |string  |    |



**schema property**




**ExchangeTrade**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
|amount | amount   |number  |    |
|buyId | buy ID   |string  |    |
|buyOrderId | buy order ID   |string  |    |
|buyTurnover | buy turnover   |number  |    |
|direction | direction,value:BUY,SELL   |string  |    |
|id | trade ID   |string  |    |
|price | price   |number  |    |
|sellId | sell ID   |string  |    |
|sellOrderId | sell order ID   |string  |    |
|sellTurnover | sell turnover   |number  |    |
|symbol | trading pair   |string  |    |
|time | timestamp   |integer(int64)  |    |



## Market Data Overview


**Interface Description**:


**Interface URL**:`/openapi/v1/market/overview`


**Request Method**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**Request Param**：
N/A at this time



**Return Example**:

```json
{
	"code": "",
	"data": {
		"additionalProperties1": [
			{
				"baseSymbol": "",
				"baseUsdRate": 0,
				"change": 0,
				"chg": 0,
				"close": 0,
				"coinSymbol": "",
				"high": 0,
				"lastDayClose": 0,
				"low": 0,
				"open": 0,
				"symbol": "",
				"turnover": 0,
				"usdRate": 0,
				"volume": 0
			}
		]
	},
	"description": ""
}
```

**Return Param**:


| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
|code| return code  |string  |    |
|data| return data  |array  | CoinThumb   |
|description| return description  |string  |    |



**schema property**




**CoinThumb**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
|baseSymbol | base coin symbol   |string  |    |
|baseUsdRate | base coin USD exchange rate   |number  |    |
|change | change   |number  |    |
|chg | change percentage   |number  |    |
|close | close price   |number  |    |
|coinSymbol | trading pair   |string  |    |
|high | high price   |number  |    |
|lastDayClose | previous day close price   |number  |    |
|low | low price   |number  |    |
|open | open price   |number  |    |
|symbol | trading pair   |string  |    |
|turnover | turnover   |number  |    |
|usdRate | traded coin USD exchange rate   |number  |    |
|volume | trade volume   |number  |    |



# order


## Cancel Order


**Interface Description**:


**Interface URL**:`/openapi/v1/order/cancel`


**Request Method**：`POST`


**consumes**:`["application/json"]`


**produces**:`["*/*","application/json"]`


**Request Example**：
```json
{
	"orderId": "",
	"source": "",
	"token": "",
	"userId": ""
}
```


**Request Param**：

| Param Name         | Param Desc     |     in |  Mandatory      |  Data Type  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|orderId| order ID  | body | true |string  |    |



**Return Example**:

```json
{
	"code": "",
	"data": {},
	"description": ""
}
```

**Return Param**:


| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
|code| return code  |string  |    |
|data| return data  |object  |    |
|description| return description  |string  |    |





## Request Current Orders


**Interface Description**:


**Interface URL**:`/openapi/v1/order/current`


**Request Method**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**Request Param**：

| Param Name         | Param Desc     |     in |  Mandatory      |  Data Type  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|pageNo| page number  | query | false |integer  |    |
|pageSize| page size  | query | false |integer  |    |
|symbol| trading pair  | query | false |string  |    |

**Return Example**:

```json
{
	"code": "",
	"data": {
		"content": [
			{
				"amount": 0,
				"baseSymbol": "",
				"canceledTime": 0,
				"coinSymbol": "",
				"completed": true,
				"completedTime": 0,
				"direction": "",
				"email": "",
				"mobile": "",
				"orderId": "",
				"price": 0,
				"status": "",
				"symbol": "",
				"time": 0,
				"tradedAmount": 0,
				"turnover": 0,
				"type": "",
				"useDiscount": "",
				"userId": ""
			}
		],
		"first": true,
		"last": true,
		"number": 0,
		"numberOfElements": 0,
		"size": 0,
		"sort": {},
		"totalElements": 0,
		"totalPages": 0
	},
	"description": ""
}
```

**Return Param**:


| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
|code| return code  |string  |    |
|data| return data  |Page«ExchangeOrder»  | Page«ExchangeOrder»   |
|description| return description  |string  |    |



**schema property**




**Page«ExchangeOrder»**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
|content |    |array  | ExchangeOrder   |
|first |    |boolean  |    |
|last |    |boolean  |    |
|number |    |integer(int32)  |    |
|numberOfElements |    |integer(int32)  |    |
|size |    |integer(int32)  |    |
|sort |    |Sort  | Sort   |
|totalElements |    |integer(int64)  |    |
|totalPages |    |integer(int32)  |    |

**ExchangeOrder**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
|amount | amount   |number  |    |
|baseSymbol | base coin symbold   |string  |    |
|canceledTime | cancel timestamp   |integer(int64)  |    |
|coinSymbol | coin symbol   |string  |    |
|completed |    |boolean  |    |
|completedTime | complete timestamp   |integer(int64)  |    |
|direction | direction,value:BUY,SELL   |string  |    |
|email |    |string  |    |
|mobile |    |string  |    |
|orderId | order ID   |string  |    |
|price | order price   |number  |    |
|status | order status,value:'TRADING': 'trading', 'COMPLETED': 'completed', 'CANCELED': 'canceled', 'PARTFILLED': 'partfilled', 'PARTFILL_CANCELD': 'partfilled canceled', 'OVERTIMED': 'overtimed'   |string  |    |
|symbol | trading pair   |string  |    |
|time | order timestamp   |integer(int64)  |    |
|tradedAmount | trade volume   |number  |    |
|turnover | turnover  |number  |    |
|type | order type,value:MARKET_PRICE,LIMIT_PRICE   |string  |    |
|useDiscount | discount used (0 No, 1Yes)   |string  |    |
|userId | user ID   |string  |    |

**Sort**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |




## Request Historic Orders


**Interface Description**:


**Interface URL**:`/openapi/v1/order/history`


**Request Method**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**Request Param**：

| Param Name         | Param Desc     |     in |  Mandatory      |  Data Type  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|pageNo| page number  | query | false |integer  |    |
|pageSize| page size  | query | false |integer  |    |
|symbol| trading pair  | query | false |string  |    |

**Return Example**:

```json
{
	"code": "",
	"data": {
		"content": [
			{
				"amount": 0,
				"baseSymbol": "",
				"canceledTime": 0,
				"coinSymbol": "",
				"completed": true,
				"completedTime": 0,
				"direction": "",
				"email": "",
				"mobile": "",
				"orderId": "",
				"price": 0,
				"status": "",
				"symbol": "",
				"time": 0,
				"tradedAmount": 0,
				"turnover": 0,
				"type": "",
				"useDiscount": "",
				"userId": ""
			}
		],
		"first": true,
		"last": true,
		"number": 0,
		"numberOfElements": 0,
		"size": 0,
		"sort": {},
		"totalElements": 0,
		"totalPages": 0
	},
	"description": ""
}
```

**Return Param**:


| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
|code| return code  |string  |    |
|data| return data  |Page«ExchangeOrder»  | Page«ExchangeOrder»   |
|description| return description  |string  |    |



**schema property**




**Page«ExchangeOrder»**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
|content |    |array  | ExchangeOrder   |
|first |    |boolean  |    |
|last |    |boolean  |    |
|number |    |integer(int32)  |    |
|numberOfElements |    |integer(int32)  |    |
|size |    |integer(int32)  |    |
|sort |    |Sort  | Sort   |
|totalElements |    |integer(int64)  |    |
|totalPages |    |integer(int32)  |    |

**ExchangeOrder**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
|amount | amount   |number  |    |
|baseSymbol | base coin symbol   |string  |    |
|canceledTime | cancel timestamp   |integer(int64)  |    |
|coinSymbol | coin symbol   |string  |    |
|completed |    |boolean  |    |
|completedTime | completed timestamp   |integer(int64)  |    |
|direction | direction,value:BUY,SELL   |string  |    |
|email |    |string  |    |
|mobile |    |string  |    |
|orderId | order ID   |string  |    |
|price | order price   |number  |    |
|status | order status,value:'TRADING': 'trading', 'COMPLETED': 'completed', 'CANCELED': 'canceled', 'PARTFILLED': 'partfilled', 'PARTFILL_CANCELD': 'partfilled canceled', 'OVERTIMED': 'overtimed'   |string  |    |
|symbol | trading pair   |string  |    |
|time | order timestamp   |integer(int64)  |    |
|tradedAmount | trade volume   |number  |    |
|turnover | turnover   |number  |    |
|type | order type,value:MARKET_PRICE,LIMIT_PRICE   |string  |    |
|useDiscount | discount used(0 No, 1 Yes)   |string  |    |


**Sort**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |





## Request Order Details


**Interface Description**:


**Interface URL**:`/openapi/v1/order/orderDetail`


**Request Method**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**Request Param**：

| Param Name         | Param Desc     |     in |  Mandatory      |  Data Type  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|orderId| ID  | query | true |string  |    |

**Return Example**:

```json
{
	"code": "",
	"data": {
		"amount": 0,
		"baseSymbol": "",
		"canceledTime": 0,
		"coinSymbol": "",
		"completed": true,
		"completedTime": 0,
		"direction": "",
		"email": "",
		"mobile": "",
		"orderId": "",
		"price": 0,
		"status": "",
		"symbol": "",
		"time": 0,
		"tradedAmount": 0,
		"turnover": 0,
		"type": "",
		"useDiscount": "",
		"userId": ""
	},
	"description": ""
}
```

**Return Param**:


| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
|code| return code  |string  |    |
|data| return data  |ExchangeOrder  | ExchangeOrder   |
|description| return description  |string  |    |



**schema property**




**ExchangeOrder**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
|amount | amount   |number  |    |
|baseSymbol | base coin symbol   |string  |    |
|canceledTime | cancel timestamp   |integer(int64)  |    |
|coinSymbol | coin symbol   |string  |    |
|completed |    |boolean  |    |
|completedTime | completed timestamp   |integer(int64)  |    |
|direction | direction,value:BUY,SELL   |string  |    |
|email |    |string  |    |
|mobile |    |string  |    |
|orderId | order ID   |string  |    |
|price | order price   |number  |    |
|status | order status,value:'TRADING': 'trading', 'COMPLETED': 'completed', 'CANCELED': 'canceled', 'PARTFILLED': 'partfilled', 'PARTFILL_CANCELD': 'partfilled cancelled', 'OVERTIMED': 'overtimed'   |string  |    |
|symbol | trading pair   |string  |    |
|time | order timestamp   |integer(int64)  |    |
|tradedAmount | trade volume   |number  |    |
|turnover | turnover  |number  |    |
|type | order type,value:MARKET_PRICE,LIMIT_PRICE   |string  |    |
|useDiscount | discount used (0 No, 1 Yes)   |string  |    |




## Submit Order


**Interface Description**:


**Interface URL**:`/openapi/v1/order/place`


**Request Method**：`POST`


**consumes**:`["application/json"]`


**produces**:`["*/*","application/json"]`



**Request Param**：

| Param Name         | Param Desc     |     in |  Mandatory      |  Data Type  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|amount| order amount  | query | true |string  |    |
|direction| direction(0 buy, 1 sell),value:0,1  | query | true |string  |    |
|price| order price  | query | false |string  |    |
|symbol| trading pair  | query | true |string  |    |
|type| Type(0 market, 1 limit),value:0,1  | query | true |string  |    |

**Return Example**:

```json
{
	"code": "",
	"data": "",
	"description": ""
}
```

**Return Param**:


| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
|code| return code  |string  |    |
|data| return data  |string  |    |
|description| return description  |string  |    |


# account

## Request Account Balance


**Interface Description**:


**Interface URL**:`/openapi/v1/capital/balance`


**Request Method**：`GET`


**consumes**:``


**produces**:`["application/xml","application/json"]`



**Request Param**：

| Param Name         | Param Desc     |     in |  Mandatory      |  Data Type  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |

**Return Example**:

```json
{
	"code": "",
	"data": [
		{
			"availableAmount": 1,
			"currency": "",
			"frozenAmount": 1
		}
	],
	"description": ""
}
```

**Return Param**:


| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
|code| return code  |string  |    |
|data| return data  |array  | user asset details   |
|description| return description  |string  |    |



**schema property**




**User Asset Details**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
|availableAmount | available amount   |number  |    |
|currency | coin name   |string  |    |
|frozenAmount | frozen amount  |number  |    |


## Request Deposit Address


**Interface Description**:


**Interface URL**:`/openapi/v1/capital/depositAddress`


**Request Method**：`GET`


**consumes**:``


**produces**:`["application/json"]`



**Request Param**：

| Param Name         | Param Desc     |     in |  Mandatory      |  Data Type  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|currencyName| coin name  | query | true |string  |    |

**Return Example**:

```json
{
	"code": "",
	"data": {
		"account": "",
		"address": "",
		"havaTag": ""
	},
	"description": ""
}
```

**Return Param**:


| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
|code| return code  |string  |    |
|data| return data  |request deposit address  | request deposit address   |
|description| return description  |string  |    |



**schema property**




**Request Deposit Address**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
|account | tagged coin types deposit to designated address   |string  |    |
|address | account deposit address   |string  |    |
|havaTag | have tagged address   |string  |    |


## Request Deposit History


**Interface Description**:


**Interface URL**:`/openapi/v1/capital/depositRecord`


**Request Method**：`GET`



**Request Param**：

| Param Name         | Param Desc     |     in |  Mandatory      |  Data Type  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|pageNo| page number  | query | false |integer  |    |
|pageSize| page size  | query | false |integer  |    |

**Return Example**:

```json
{
	"code": "",
	"data": {
		"endRow": 0,
		"firstPage": 0,
		"hasNextPage": true,
		"hasPreviousPage": true,
		"isFirstPage": true,
		"isLastPage": true,
		"lastPage": 0,
		"list": [
			{
				"accountAddress": "",
				"currency": "",
				"dateReceive": "",
				"id": "",
				"receiveAmount": 0,
				"serialNumber": "",
				"state": ""
			}
		],
		"navigateFirstPage": 0,
		"navigateLastPage": 0,
		"navigatePages": 0,
		"navigatepageNums": [],
		"nextPage": 0,
		"pageNum": 0,
		"pageSize": 0,
		"pages": 0,
		"prePage": 0,
		"size": 0,
		"startRow": 0,
		"total": 0
	},
	"description": ""
}
```

**Return Param**:


| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
|code| return code  |string  |    |
|data| return data  |PageInfo«deposit history details»  | PageInfo«deposit history details»   |
|description| return description  |string  |    |



**schema property**




**PageInfo«Deposit History Details»**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
|endRow |    |integer(int32)  |    |
|firstPage |    |integer(int32)  |    |
|hasNextPage |    |boolean  |    |
|hasPreviousPage |    |boolean  |    |
|isFirstPage |    |boolean  |    |
|isLastPage |    |boolean  |    |
|lastPage |    |integer(int32)  |    |
|list |    |array  | deposit history details   |
|navigateFirstPage |    |integer(int32)  |    |
|navigateLastPage |    |integer(int32)  |    |
|navigatePages |    |integer(int32)  |    |
|navigatepageNums |    |array  |    |
|nextPage |    |integer(int32)  |    |
|pageNum |    |integer(int32)  |    |
|pageSize |    |integer(int32)  |    |
|pages |    |integer(int32)  |    |
|prePage |    |integer(int32)  |    |
|size |    |integer(int32)  |    |
|startRow |    |integer(int32)  |    |
|total |    |integer(int64)  |    |

**Deposit History Details**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
|accountAddress | deposit address   |string  |    |
|currency | deposit coin type   |string  |    |
|dateReceive | deposit timestampe   |string(date-time)  |    |
|id | ID   |string  |    |
|receiveAmount | deposit amount   |number  |    |
|serialNumber | order serial number (order id)   |string  |    |
|state | status：3 pending,    1 complete   |string  |    |


## Withdraw Request


**Interface Description**:


**Interface URL**:`/openapi/v1/capital/withdraw`


**Request Method**：`POST`


**consumes**:`["application/json"]`


**produces**:`["application/xml","application/json"]`



**Request Param**：

| Param Name         | Param Desc     |     in |  Mandatory      |  Data Type  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|address| withdraw address  | query | true |string  |    |
|currency| coin type  | query | true |string  |    |
|tag| tag value  | query | true |string  |    |
|widhdrawAmt| withdraw amount  | query | true |string  |    |

**Return Example**:

```json
{
	"code": "",
	"data": {},
	"description": ""
}
```

**Return Param**:


| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
|code| return code  |string  |    |
|data| return data  |object  |    |
|description| return description  |string  |    |






## Request Withdraw History


**Interface Description**:


**Interface URL**:`/openapi/v1/capital/withdrawRecord`


**Request Method**：`GET`


**Request Param**：

| Param Name         | Param Desc     |     in |  Mandatory      |  Data Type  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|pageNo| page number  | query | false |integer  |    |
|pageSize| page size  | query | false |integer  |    |

**Return Example**:

```json
{
	"code": "",
	"data": {
		"endRow": 0,
		"firstPage": 0,
		"hasNextPage": true,
		"hasPreviousPage": true,
		"isFirstPage": true,
		"isLastPage": true,
		"lastPage": 0,
		"list": [
			{
				"accountAddress": "",
				"actualAmount": 0,
				"applyStatus": "",
				"checkAddress": "",
				"currencyName": "",
				"dateCreate": "",
				"id": "",
				"poundage": 0,
				"tag": "",
				"txId": "",
				"withdrawAmount": 0
			}
		],
		"navigateFirstPage": 0,
		"navigateLastPage": 0,
		"navigatePages": 0,
		"navigatepageNums": [],
		"nextPage": 0,
		"pageNum": 0,
		"pageSize": 0,
		"pages": 0,
		"prePage": 0,
		"size": 0,
		"startRow": 0,
		"total": 0
	},
	"description": ""
}
```

**Return Param**:


| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
|code| return code  |string  |    |
|data| return data  |PageInfo«withdraw history details»  | PageInfo«withdraw history details»   |
|description| return description  |string  |    |



**schema property**




**PageInfo«withdraw history details»**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
|endRow |    |integer(int32)  |    |
|firstPage |    |integer(int32)  |    |
|hasNextPage |    |boolean  |    |
|hasPreviousPage |    |boolean  |    |
|isFirstPage |    |boolean  |    |
|isLastPage |    |boolean  |    |
|lastPage |    |integer(int32)  |    |
|list |    |array  | Withdraw Record   |
|navigateFirstPage |    |integer(int32)  |    |
|navigateLastPage |    |integer(int32)  |    |
|navigatePages |    |integer(int32)  |    |
|navigatepageNums |    |array  |    |
|nextPage |    |integer(int32)  |    |
|pageNum |    |integer(int32)  |    |
|pageSize |    |integer(int32)  |    |
|pages |    |integer(int32)  |    |
|prePage |    |integer(int32)  |    |
|size |    |integer(int32)  |    |
|startRow |    |integer(int32)  |    |
|total |    |integer(int64)  |    |

**Withdraw History Details**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
|accountAddress | withdraw address   |string  |    |
|actualAmount | actual amount   |number  |    |
|applyStatus | request status 1:pending review, 2:approved, 3:not approved   |string  |    |
|checkAddress | coin blockchain browser address   |string  |    |
|currencyName | coin name   |string  |    |
|dateCreate | request timestamp   |string(date-time)  |    |
|id | main id   |string  |    |
|poundage | transaction fee   |number  |    |
|tag | tag value   |string  |    |
|txId | third party transaction turnover   |string  |    |
|withdrawAmount | withdraw amount   |number  |    |




# transaction

## Request Global Remittance Setting Details

**Interface URL** `/openapi/v1/transaction/legalConf`


**Request Method** `GET`


**Request Param**

N/A at this time



**Return Param**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
| code     |return code      |    string   |       |
| data     |return data      |    array   |   global remittance currency details    |
| description     |return description      |    string   |       |
            



**schema property**
  
**Global Remittance Currency Details**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
| createAt         |     create timestamp      |  integer(int64)   |      |
| currencyId         |     stablecoin ID      |  string   |      |
| currencyName         |     stablecoin name      |  string   |      |
| exportChannelRate         |     sell channel fee      |  number   |      |
| exportExcRate         |     sell exchange rate      |  number   |      |
| exportMaxAmount         |     sell single max amount      |  number   |      |
| exportMinAmount         |     sell single min amount      |  number   |      |
| exportStatus         |     sell staus: 1.enable; 2.disable;      |  string   |      |
| id         |     currency ID      |  string   |      |
| importChannelRate         |     buy channel fee      |  number   |      |
| importExcRate         |     buy exchange rate      |  number   |      |
| importMaxAmount         |     buy single max amount      |  number   |      |
| importMinAmount         |     buy single min amount      |  number   |      |
| importStatus         |     buy status: 1.enable; 2.disable;      |  string   |      |
| logoUrl         |     logo picture url      |  string   |      |
| name         |     currency name      |  string   |      |
| projectName         |     project name      |  string   |      |
            




**Return Example**


```json
{
	"code": "",
	"data": [
		{
			"createAt": 0,
			"currencyId": "",
			"currencyName": "",
			"exportChannelRate": 1,
			"exportExcRate": 1,
			"exportMaxAmount": 1,
			"exportMinAmount": 1,
			"exportStatus": "",
			"id": "",
			"importChannelRate": 1,
			"importExcRate": 1,
			"importMaxAmount": 1,
			"importMinAmount": 1,
			"importStatus": "",
			"logoUrl": "",
			"name": "",
			"projectName": ""
		}
	],
	"description": ""
}
```


## Buy Order

**Interface URL** `/openapi/v1/transaction/in`


**Request Method** `POST`


**Interface Description** 


**Request Param**

| Param Name         | Param Desc     |     Request Type |  Mandatory      |  Data Type   |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
| legalAmount         |      currency amount   |     query        |       true      | number   |      |
| legalCurrenyId         |      currency ID   |     query        |       true      | string   |      |



**Return Param**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
| code     |return code      |    string   |       |
| data     |return data      |    submit transaction details   |   submit transaction details    |
| description     |return description      |    string   |       |
            

**schema property**
  
**Submit Transaction Details**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
| bankSerialNumber         |     bank serial number      |  string   |      |
| channelFee         |     channel fee      |  number   |      |
| channelFeeRate         |     channel fee rate      |  number   |      |
| createAt         |     create timestamp      |  integer(int64)   |      |
| currencyAmount         |     stablecoin amount      |  number   |      |
| currencyId         |     stablecoin ID      |  string   |      |
| currenyName         |     stablecoin name      |  string   |      |
| exchRate         |     current exchange rate      |  number   |      |
| fee         |     transaction fee（deducted transaction fee）      |  number   |      |
| id         |     main ID      |  string   |      |
| legalAmount         |     currency amount      |  number   |      |
| legalCurrenyId         |     currency ID      |  string   |      |
| legalCurrenyName         |     currency name      |  string   |      |
| noteCode         |     bank transfer referral code      |  string   |      |
| originalCurrencyAmount         |     original stablecoin amount      |  number   |      |
| payAt         |     payment timestamp      |  integer(int64)   |      |
| payBirthDate         |     sender birthdate(yyyy-MM-dd)      |  string   |      |
| payCountry         |     sender nationality      |  string   |      |
| payDeadline         |     payment deadline      |  integer(int64)   |      |
| payFirstName         |     sender first name      |  string   |      |
| payLastName         |     sender last name      |  string   |      |
| payMiddleName         |     sender middle name      |  string   |      |
| payType         |     payment method 1.bank transfer 2.wire transfer 3.credit card      |  string   |      |
| receiveAccount         |     platform bank account      |  platform bank account   | platform bank account     |
| receiveId         |     platform bank account ID      |  string   |      |
| remark         |     remark      |  string   |      |
| source         |     source: 1.PC 3.android 4.apple 5.wechat 6.H5      |  string   |      |
| status         |     status: 1.pending payment 2. timeout 3.canceled 4.pending review 5.rejected 6.complete      |  string   |      |
| transactionType         |     transaction type: 1.Buy; 2.Sell;      |  string   |      |
| userCode         |     UID      |  string   |      |
| userId         |     user ID      |  string   |      |
| verifiedAt         |     review timestamp      |  integer(int64)   |      |
| verifiedDescCn         |     review details(chinese)      |  string   |      |
| verifiedDescEs         |     review details(english)      |  string   |      |
            

**Platform Bank Account**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
| address         |     beneficiary address      |  string   |      |
| bankAddress         |     beneficiary bank address      |  string   |      |
| bankCardNo         |     beneficiary bank account number      |  string   |      |
| bankCity         |     beneficiary bank city      |  string   |      |
| bankCountry         |     beneficiary bank country      |  string   |      |
| bankName         |     beneficiary bank name      |  string   |      |
| bankProvince         |     beneficiary bank province      |  string   |      |
| bankSwiftCode         |     beneficiary bank Swift code      |  string   |      |
| city         |     beneficiary city      |  string   |      |
| country         |     beneficiary country      |  string   |      |
| createAt         |     create timestamp      |  integer(int64)   |      |
| firstName         |     beneficiary name      |  string   |      |
| id         |     main ID      |  string   |      |
| lastModifyAt         |     last modified timestamp      |  integer(int64)   |      |
| lastName         |     beneficiary last name      |  string   |      |
| middleName         |     beneficiary middle name      |  string   |      |
| province         |     beneficiary province      |  string   |      |
| remittanceType         |     remittance type：1.PH Local; 2.Swift      |  string   |      |
| symbol         |     asset type(currently only support USD and PHP)      |  string   |      |
| type         |     account type: 1. system account; 2.platform user;      |  string   |      |
| userId         |     user ID      |  string   |      |
            

**Return Example**


```json
{
	"code": "",
	"data": {
		"bankSerialNumber": "",
		"channelFee": 1,
		"channelFeeRate": 1,
		"createAt": 0,
		"currencyAmount": 1,
		"currencyId": "",
		"currenyName": "",
		"exchRate": 1,
		"fee": 1,
		"id": "",
		"legalAmount": 1,
		"legalCurrenyId": "",
		"legalCurrenyName": "",
		"noteCode": "",
		"originalCurrencyAmount": 1,
		"payAt": 0,
		"payBirthDate": "",
		"payCountry": "",
		"payDeadline": 0,
		"payFirstName": "",
		"payLastName": "",
		"payMiddleName": "",
		"payType": "",
		"receiveAccount": {
			"address": "",
			"bankAddress": "",
			"bankCardNo": "",
			"bankCity": "",
			"bankCountry": "",
			"bankName": "",
			"bankProvince": "",
			"bankSwiftCode": "",
			"city": "",
			"country": "",
			"createAt": 0,
			"firstName": "",
			"id": "",
			"lastModifyAt": 0,
			"lastName": "",
			"middleName": "",
			"province": "",
			"remittanceType": "",
			"symbol": "",
			"type": "",
			"userId": ""
		},
		"receiveId": "",
		"remark": "",
		"source": "",
		"status": "",
		"transactionType": "",
		"userCode": "",
		"userId": "",
		"verifiedAt": 0,
		"verifiedDescCn": "",
		"verifiedDescEs": ""
	},
	"description": ""
}
```


## Sell Order

**Interface URL** `/openapi/v1/transaction/out`


**Request Method** `POST`



**Interface Description** 

**Request Param**

| Param Name         | Param Desc     |     Request Type |  Mandatory      |  Data Type   |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
| address         |      beneficiary address   |     query        |       true      | string   |      |
| bankAddress         |      beneficiary bank address   |     query        |       false      | string   |      |
| bankCardNo         |      beneficiary bank account   |     query        |       true      | string   |      |
| bankCity         |      beneficiary bank city   |     query        |       false      | string   |      |
| bankCountry         |      beneficiary bank country   |     query        |       false      | string   |      |
| bankName         |      beneficiary bank name   |     query        |       true      | string   |      |
| bankProvince         |      beneficiary bank province   |     query        |       false      | string   |      |
| bankSwiftCode         |      beneficiary bank Swift code   |     query        |       false      | string   |      |
| city         |      beneficiary city   |     query        |       true      | string   |      |
| country         |      beneficiary country   |     query        |       true      | string   |      |
| currencyAmount         |      stablecoin amount   |     query        |       false      | number   |      |
| firstName         |      beneficiary first name   |     query        |       true      | string   |      |
| lastName         |      beneficiary last name   |     query        |       true      | string   |      |
| legalCurrenyId         |      currency ID   |     query        |       false      | string   |      |
| locale         |      language   |     query        |       false      | string   |      |
| middleName         |      beneficiary middle name   |     query        |       false      | string   |      |
| province         |      beneficiary province   |     query        |       true      | string   |      |
| tradePwd         |      transaction password   |     query        |       false      | string   |      |
| type         |      account type: 2.platform user   |     query        |       false      | string   |      |
| symbol         |      currency type currently only support USD and PHP   |     query        |       false      | string   |      |
| remittanceType         |      remittance type：1.PH Local; 2.Swift  |     query        |       false      | string   |      |
            


**Return Param**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
| code     |return code      |    string   |       |
| data     |return data      |    submit transaction details   |   submit transaction details    |
| description     |return description      |    string   |       |




**schema property**
  
**Submit Transaction Details**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
| bankSerialNumber         |     bank serial number      |  string   |      |
| channelFee         |     channel fee      |  number   |      |
| channelFeeRate         |     channel fee rate      |  number   |      |
| createAt         |     create timestamp      |  integer(int64)   |      |
| currencyAmount         |     stablecoin amount      |  number   |      |
| currencyId         |     stablecoin ID      |  string   |      |
| currenyName         |     stablecoin name      |  string   |      |
| exchRate         |     current exchange rate      |  number   |      |
| fee         |     transaction fee（deducted transaction fee）      |  number   |      |
| id         |     main ID      |  string   |      |
| legalAmount         |     currency amount      |  number   |      |
| legalCurrenyId         |     currency ID      |  string   |      |
| legalCurrenyName         |     currency name      |  string   |      |
| noteCode         |     remittance referral code      |  string   |      |
| originalCurrencyAmount         |     amount      |  number   |      |
| payAt         |     payment timestamp      |  integer(int64)   |      |
| payBirthDate         |     sender birthday(yyyy-MM-dd)      |  string   |      |
| payCountry         |     sender nationality      |  string   |      |
| payDeadline         |     payment deadline      |  integer(int64)   |      |
| payFirstName         |     sender first name      |  string   |      |
| payLastName         |     sender last name      |  string   |      |
| payMiddleName         |     sender middle name      |  string   |      |
| payType         |     payment method 1.bank transfer 2.SWIFT transfer 3.credit card      |  string   |      |
| receiveAccount         |     platform bank account      |  platform bank account   | platform bank account     |
| receiveId         |     platform bank account ID      |  string   |      |
| remark         |     remark      |  string   |      |
| source         |     source: 1.PC 3.android 4.apple 5.wechat 6.H5      |  string   |      |
| status         |     status: 1.pending payment 2.timeout 3.canceld 4.pending review 5.rejected 6.complete      |  string   |      |
| transactionType         |     transaction type: 1.Buy; 2.Sell;      |  string   |      |
| userCode         |     UID      |  string   |      |
| userId         |     User ID      |  string   |      |
| verifiedAt         |     review timestamp      |  integer(int64)   |      |
| verifiedDescCn         |     review details(chinese)      |  string   |      |
| verifiedDescEs         |     review details(english)      |  string   |      |
            

**Platform Bank Account**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
| address         |     beneficiary address      |  string   |      |
| bankAddress         |     beneficiary bank address      |  string   |      |
| bankCardNo         |     beneficiary bank account      |  string   |      |
| bankCity         |     beneficiary bank city      |  string   |      |
| bankCountry         |     beneficiary bank country      |  string   |      |
| bankName         |     beneficiary bank name      |  string   |      |
| bankProvince         |     beneficiary bank province      |  string   |      |
| bankSwiftCode         |     beneficiary bank SWIFT code      |  string   |      |
| city         |     beneficiary city      |  string   |      |
| country         |     beneficiary country      |  string   |      |
| createAt         |     create timestamp      |  integer(int64)   |      |
| firstName         |     beneficiary first name      |  string   |      |
| id         |     main ID      |  string   |      |
| lastModifyAt         |     last modified time      |  integer(int64)   |      |
| lastName         |     beneficiary last name      |  string   |      |
| middleName         |     beneficiary middle name      |  string   |      |
| province         |     beneficiary province      |  string   |      |
| remittanceType         |     remittance type：1.PH Local; 2.Swift      |  string   |      |
| symbol         |     asset type(currently only support USD and PHP)      |  string   |      |
| type         |     account type: 1. system account ; 2.platform user;      |  string   |      |
| userId         |     user ID      |  string   |      |
            




**Return Example**


```json
{
	"code": "",
	"data": {
		"bankSerialNumber": "",
		"channelFee": 1,
		"channelFeeRate": 1,
		"createAt": 0,
		"currencyAmount": 1,
		"currencyId": "",
		"currenyName": "",
		"exchRate": 1,
		"fee": 1,
		"id": "",
		"legalAmount": 1,
		"legalCurrenyId": "",
		"legalCurrenyName": "",
		"noteCode": "",
		"originalCurrencyAmount": 1,
		"payAt": 0,
		"payBirthDate": "",
		"payCountry": "",
		"payDeadline": 0,
		"payFirstName": "",
		"payLastName": "",
		"payMiddleName": "",
		"payType": "",
		"receiveAccount": {
			"address": "",
			"bankAddress": "",
			"bankCardNo": "",
			"bankCity": "",
			"bankCountry": "",
			"bankName": "",
			"bankProvince": "",
			"bankSwiftCode": "",
			"city": "",
			"country": "",
			"createAt": 0,
			"firstName": "",
			"id": "",
			"lastModifyAt": 0,
			"lastName": "",
			"middleName": "",
			"province": "",
			"remittanceType": "",
			"symbol": "",
			"type": "",
			"userId": ""
		},
		"receiveId": "",
		"remark": "",
		"source": "",
		"status": "",
		"transactionType": "",
		"userCode": "",
		"userId": "",
		"verifiedAt": 0,
		"verifiedDescCn": "",
		"verifiedDescEs": ""
	},
	"description": ""
}
```


## Cancel Order

**Interface URL** `/openapi/v1/transaction/cancel`


**Request Method** `POST`


**Interface Description** 

**Request Param**

| Param Name         | Param Desc     |     Request Type |  Mandatory      |  Data Type   |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
| id         |      Main ID   |     query        |       true      | string   |      |       



**Return Param**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
| code     |return code      |    string   |       |
| data     |return data      |    object   |       |
| description     |return description      |    string   |       |





**Return Example**


```json
{
	"code": "",
	"data": {},
	"description": ""
}
```


## Paid Order

**Interface URL** `/openapi/v1/transaction/pay`


**Request Method** `POST`


**Interface Description** 

**Request Param**

| Param Name         | Param Desc     |     Request Type |  Mandatory      |  Data Type   |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
| apiKey         |      apiKey   |     header        |       true      | string   |      |
| id         |      Main ID   |     query        |       true      | string   |      |


**Return Param**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
| code     |return code      |    string   |       |
| data     |return data      |    object   |       |
| description     |return description      |    string   |       |
            

**Return Example**


```json
{
	"code": "",
	"data": null,
	"description": ""
}
```


## Request Transaction (Buy、Sell) History

**Interface URL** `/openapi/v1/transaction/transactionList`


**Request Method** `POST`




**Interface Description** 

**Request Param**

| Param Name         | Param Desc     |     Request Type |  Mandatory      |  Data Type   |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
| pageNo         |      page number   |     query        |       false      | integer   |      |
| pageSize         |      page size   |     query        |       false      | integer   |      |
| statuses         |      status: 1.pending payment 2.timedout 3.canceled 4.pending review 5.rejected 6.complete   |     query        |       false      | array   | string     |
            


**Return Param**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | -------------------|-------|----------- |
| code     |return code      |    string   |       |
| data     |return data      |    PageInfo«submit transaction details»   |   PageInfo«submit transaction details»    |
| description     |return description      |    string   |       |
            



**schema property**
  
**PageInfo«submit transaction details»**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
| endRow         |           |  integer(int32)   |      |
| firstPage         |           |  integer(int32)   |      |
| hasNextPage         |           |  boolean   |      |
| hasPreviousPage         |           |  boolean   |      |
| isFirstPage         |           |  boolean   |      |
| isLastPage         |           |  boolean   |      |
| lastPage         |           |  integer(int32)   |      |
| list         |           |  array   | submit transaction details     |
| navigateFirstPage         |           |  integer(int32)   |      |
| navigateLastPage         |           |  integer(int32)   |      |
| navigatePages         |           |  integer(int32)   |      |
| navigatepageNums         |           |  array   |      |
| nextPage         |           |  integer(int32)   |      |
| pageNum         |           |  integer(int32)   |      |
| pageSize         |           |  integer(int32)   |      |
| pages         |           |  integer(int32)   |      |
| prePage         |           |  integer(int32)   |      |
| size         |           |  integer(int32)   |      |
| startRow         |           |  integer(int32)   |      |
| total         |           |  integer(int64)   |      |


**Submit Transaction Details**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
| bankSerialNumber         |     bank serial number      |  string   |      |
| channelFee         |     channel fee      |  number   |      |
| channelFeeRate         |     channel fee rate      |  number   |      |
| createAt         |     create timestamp      |  integer(int64)   |      |
| currencyAmount         |     stablecoin amount      |  number   |      |
| currencyId         |     stablecoin ID      |  string   |      |
| currenyName         |     stablecoin name      |  string   |      |
| exchRate         |     current exchange rate      |  number   |      |
| fee         |     transaction fee（deducted transaction fee）      |  number   |      |
| id         |     main ID      |  string   |      |
| legalAmount         |     currency amount      |  number   |      |
| legalCurrenyId         |     currency ID      |  string   |      |
| legalCurrenyName         |     currency name      |  string   |      |
| noteCode         |     bank transfer referral code      |  string   |      |
| originalCurrencyAmount         |     original stablecoin amount      |  number   |      |
| payAt         |     payment time      |  integer(int64)   |      |
| payBirthDate         |     sender birth date (yyyy-MM-dd)      |  string   |      |
| payCountry         |     sender nationality      |  string   |      |
| payDeadline         |     payment deadline      |  integer(int64)   |      |
| payFirstName         |     sender first name      |  string   |      |
| payLastName         |     sender last name      |  string   |      |
| payMiddleName         |     sender middle name      |  string   |      |
| payType         |     payment method 1.bank transfer 2.wire transfer 3.credit card      |  string   |      |
| receiveAccount         |     platform bank account      |  platform bank account   | platform bank account     |
| receiveId         |     platform bank account ID      |  string   |      |
| remark         |     remark      |  string   |      |
| source         |     source: 1.PC 3.Android 4.Apple 5.Wechat 6.H5      |  string   |      |
| status         |     status: 1.pending payment 2.timedout 3.canceled 4.pending review 5.rejected 6.complete      |  string   |      |
| transactionType         |     transaction type: 1.Buy; 2.Sell;      |  string   |      |
| userCode         |     UID      |  string   |      |
| userId         |     User ID      |  string   |      |
| verifiedAt         |     review timestamp      |  integer(int64)   |      |
| verifiedDescCn         |     review details(chinese)      |  string   |      |
| verifiedDescEs         |     review details(english)      |  string   |      |
            

**Platform Bank Account**

| Param Name         | Param Desc                             |    Type |  schema |
| ------------ | ------------------|--------|----------- |
| address         |     beneficiary address      |  string   |      |
| bankAddress         |     beneficiary bank address      |  string   |      |
| bankCardNo         |     beneficiary bank account      |  string   |      |
| bankCity         |     beneficiary bank city      |  string   |      |
| bankCountry         |     beneficiary bank country      |  string   |      |
| bankName         |     beneficiary bank name      |  string   |      |
| bankProvince         |     beneficiary bank province      |  string   |      |
| bankSwiftCode         |     beneficiary bank SWIFT code     |  string   |      |
| city         |     beneficiary city      |  string   |      |
| country         |     beneficiary country      |  string   |      |
| createAt         |     create timstamp      |  integer(int64)   |      |
| firstName         |     beneficiary first name      |  string   |      |
| id         |     main ID      |  string   |      |
| lastModifyAt         |     last modified time      |  integer(int64)   |      |
| lastName         |     beneficiary last name      |  string   |      |
| middleName         |     beneficiary middle name      |  string   |      |
| province         |     beneficiary province      |  string   |      |
| remittanceType         |     remittance type：1.PH Local; 2.Swift      |  string   |      |
| symbol         |     asset type(currently only support USD and PHP)      |  string   |      |
| type         |     account type: 1. System Account; 2.Platform User;      |  string   |      |
| userId         |     user ID      |  string   |      |
            




**Return Example**


```json
{
	"code": "",
	"data": {
		"endRow": 0,
		"firstPage": 0,
		"hasNextPage": true,
		"hasPreviousPage": true,
		"isFirstPage": true,
		"isLastPage": true,
		"lastPage": 0,
		"list": [
			{
				"bankSerialNumber": "",
				"channelFee": 1,
				"channelFeeRate": 1,
				"createAt": 0,
				"currencyAmount": 1,
				"currencyId": "",
				"currenyName": "",
				"exchRate": 1,
				"fee": 1,
				"id": "",
				"legalAmount": 1,
				"legalCurrenyId": "",
				"legalCurrenyName": "",
				"noteCode": "",
				"originalCurrencyAmount": 1,
				"payAt": 0,
				"payBirthDate": "",
				"payCountry": "",
				"payDeadline": 0,
				"payFirstName": "",
				"payLastName": "",
				"payMiddleName": "",
				"payType": "",
				"receiveAccount": {
					"address": "",
					"bankAddress": "",
					"bankCardNo": "",
					"bankCity": "",
					"bankCountry": "",
					"bankName": "",
					"bankProvince": "",
					"bankSwiftCode": "",
					"city": "",
					"country": "",
					"createAt": 0,
					"firstName": "",
					"id": "",
					"lastModifyAt": 0,
					"lastName": "",
					"middleName": "",
					"province": "",
					"remittanceType": "",
					"symbol": "",
					"type": "",
					"userId": ""
				},
				"receiveId": "",
				"remark": "",
				"source": "",
				"status": "",
				"transactionType": "",
				"userCode": "",
				"userId": "",
				"verifiedAt": 0,
				"verifiedDescCn": "",
				"verifiedDescEs": ""
			}
		],
		"navigateFirstPage": 0,
		"navigateLastPage": 0,
		"navigatePages": 0,
		"navigatepageNums": [],
		"nextPage": 0,
		"pageNum": 0,
		"pageSize": 0,
		"pages": 0,
		"prePage": 0,
		"size": 0,
		"startRow": 0,
		"total": 0
	},
	"description": ""
}
```


