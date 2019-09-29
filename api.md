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

| Param Name         | 参数说明     |     in |  是否必须      |  数据类型  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|size| 大小  | query | true |ref  |    |
|symbol| 交易对  | query | true |string  |    |

**响应示例**:

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

**响应参数**:


| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
|code| 响应代码  |string  |    |
|data| 响应数据  |array  | ExchangeTrade   |
|description| 响应描述  |string  |    |



**schema属性说明**




**ExchangeTrade**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
|amount | 数量   |number  |    |
|buyId | 买方ID   |string  |    |
|buyOrderId | 买方订单号   |string  |    |
|buyTurnover | 买成交额   |number  |    |
|direction | 方向,可用值:BUY,SELL   |string  |    |
|id | 交易ID   |string  |    |
|price | 价格   |number  |    |
|sellId | 卖方ID   |string  |    |
|sellOrderId | 卖方订单号   |string  |    |
|sellTurnover | 卖成交额   |number  |    |
|symbol | 交易对   |string  |    |
|time | 时间戳   |integer(int64)  |    |



## 行情概览


**接口描述**:


**接口地址**:`/openapi/v1/market/overview`


**请求方式**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**请求参数**：
暂无



**响应示例**:

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

**响应参数**:


| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
|code| 响应代码  |string  |    |
|data| 响应数据  |array  | CoinThumb   |
|description| 响应描述  |string  |    |



**schema属性说明**




**CoinThumb**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
|baseSymbol | 基础币种   |string  |    |
|baseUsdRate | 基础币种对usd汇率   |number  |    |
|change | 涨跌幅   |number  |    |
|chg | 涨跌幅百分比   |number  |    |
|close | 收盘价   |number  |    |
|coinSymbol | 交易币种   |string  |    |
|high | 最高价   |number  |    |
|lastDayClose | 昨日收盘价   |number  |    |
|low | 最低价   |number  |    |
|open | 开盘价   |number  |    |
|symbol | 交易对   |string  |    |
|turnover | 交易额   |number  |    |
|usdRate | 交易币对usd汇率   |number  |    |
|volume | 交易量   |number  |    |



# order


## 撤销订单


**接口描述**:


**接口地址**:`/openapi/v1/order/cancel`


**请求方式**：`POST`


**consumes**:`["application/json"]`


**produces**:`["*/*","application/json"]`


**请求示例**：
```json
{
	"orderId": "",
	"source": "",
	"token": "",
	"userId": ""
}
```


**请求参数**：

| 参数名称         | 参数说明     |     in |  是否必须      |  数据类型  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|orderId| 订单ID  | body | true |string  |    |



**响应示例**:

```json
{
	"code": "",
	"data": {},
	"description": ""
}
```

**响应参数**:


| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
|code| 响应代码  |string  |    |
|data| 响应数据  |object  |    |
|description| 响应描述  |string  |    |





## 查询当前委托


**接口描述**:


**接口地址**:`/openapi/v1/order/current`


**请求方式**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**请求参数**：

| 参数名称         | 参数说明     |     in |  是否必须      |  数据类型  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|pageNo| 页码  | query | false |integer  |    |
|pageSize| 每页条数  | query | false |integer  |    |
|symbol| 交易对  | query | false |string  |    |

**响应示例**:

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

**响应参数**:


| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
|code| 响应代码  |string  |    |
|data| 响应数据  |Page«ExchangeOrder»  | Page«ExchangeOrder»   |
|description| 响应描述  |string  |    |



**schema属性说明**




**Page«ExchangeOrder»**

| 参数名称         | 参数说明                             |    类型 |  schema |
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

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
|amount | 数量   |number  |    |
|baseSymbol | 结算币单位   |string  |    |
|canceledTime | 取消时间戳   |integer(int64)  |    |
|coinSymbol | 币单位   |string  |    |
|completed |    |boolean  |    |
|completedTime | 交易完成时间戳   |integer(int64)  |    |
|direction | 订单方向,可用值:BUY,SELL   |string  |    |
|email |    |string  |    |
|mobile |    |string  |    |
|orderId | 订单ID   |string  |    |
|price | 挂单价格   |number  |    |
|status | 订单状态,可用值:'TRADING': '交易中', 'COMPLETED': '已完成', 'CANCELED': '已撤销', 'PARTFILLED': '部分成交', 'PARTFILL_CANCELD': '部分成交撤销', 'OVERTIMED': '已超时'   |string  |    |
|symbol | 交易对   |string  |    |
|time | 挂单时间戳   |integer(int64)  |    |
|tradedAmount | 成交量   |number  |    |
|turnover | 成交额   |number  |    |
|type | 订单类型,可用值:MARKET_PRICE,LIMIT_PRICE   |string  |    |
|useDiscount | 是否使用折扣(0不使用1使用)   |string  |    |
|userId | 用户ID   |string  |    |

**Sort**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |




## 查询历史委托


**接口描述**:


**接口地址**:`/openapi/v1/order/history`


**请求方式**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**请求参数**：

| 参数名称         | 参数说明     |     in |  是否必须      |  数据类型  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|pageNo| 页码  | query | false |integer  |    |
|pageSize| 每页条数  | query | false |integer  |    |
|symbol| 交易对  | query | false |string  |    |

**响应示例**:

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

**响应参数**:


| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
|code| 响应代码  |string  |    |
|data| 响应数据  |Page«ExchangeOrder»  | Page«ExchangeOrder»   |
|description| 响应描述  |string  |    |



**schema属性说明**




**Page«ExchangeOrder»**

| 参数名称         | 参数说明                             |    类型 |  schema |
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

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
|amount | 数量   |number  |    |
|baseSymbol | 结算币单位   |string  |    |
|canceledTime | 取消时间戳   |integer(int64)  |    |
|coinSymbol | 币单位   |string  |    |
|completed |    |boolean  |    |
|completedTime | 交易完成时间戳   |integer(int64)  |    |
|direction | 订单方向,可用值:BUY,SELL   |string  |    |
|email |    |string  |    |
|mobile |    |string  |    |
|orderId | 订单ID   |string  |    |
|price | 挂单价格   |number  |    |
|status | 订单状态,可用值:'TRADING': '交易中', 'COMPLETED': '已完成', 'CANCELED': '已撤销', 'PARTFILLED': '部分成交', 'PARTFILL_CANCELD': '部分成交撤销', 'OVERTIMED': '已超时'   |string  |    |
|symbol | 交易对   |string  |    |
|time | 挂单时间戳   |integer(int64)  |    |
|tradedAmount | 成交量   |number  |    |
|turnover | 成交额   |number  |    |
|type | 订单类型,可用值:MARKET_PRICE,LIMIT_PRICE   |string  |    |
|useDiscount | 是否使用折扣(0不使用1使用)   |string  |    |


**Sort**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |





## 查询订单详情


**接口描述**:


**接口地址**:`/openapi/v1/order/orderDetail`


**请求方式**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**请求参数**：

| 参数名称         | 参数说明     |     in |  是否必须      |  数据类型  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|orderId| 订单ID  | query | true |string  |    |

**响应示例**:

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

**响应参数**:


| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
|code| 响应代码  |string  |    |
|data| 响应数据  |ExchangeOrder  | ExchangeOrder   |
|description| 响应描述  |string  |    |



**schema属性说明**




**ExchangeOrder**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
|amount | 数量   |number  |    |
|baseSymbol | 结算币单位   |string  |    |
|canceledTime | 取消时间戳   |integer(int64)  |    |
|coinSymbol | 币单位   |string  |    |
|completed |    |boolean  |    |
|completedTime | 交易完成时间戳   |integer(int64)  |    |
|direction | 订单方向,可用值:BUY,SELL   |string  |    |
|email |    |string  |    |
|mobile |    |string  |    |
|orderId | 订单ID   |string  |    |
|price | 挂单价格   |number  |    |
|status | 订单状态,可用值:'TRADING': '交易中', 'COMPLETED': '已完成', 'CANCELED': '已撤销', 'PARTFILLED': '部分成交', 'PARTFILL_CANCELD': '部分成交撤销', 'OVERTIMED': '已超时'   |string  |    |
|symbol | 交易对   |string  |    |
|time | 挂单时间戳   |integer(int64)  |    |
|tradedAmount | 成交量   |number  |    |
|turnover | 成交额   |number  |    |
|type | 订单类型,可用值:MARKET_PRICE,LIMIT_PRICE   |string  |    |
|useDiscount | 是否使用折扣(0不使用1使用)   |string  |    |




## 下单


**接口描述**:


**接口地址**:`/openapi/v1/order/place`


**请求方式**：`POST`


**consumes**:`["application/json"]`


**produces**:`["*/*","application/json"]`



**请求参数**：

| 参数名称         | 参数说明     |     in |  是否必须      |  数据类型  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|amount| 下单数量  | query | true |string  |    |
|direction| 交易方向(0买1卖),可用值:0,1  | query | true |string  |    |
|price| 下单价格  | query | false |string  |    |
|symbol| 交易对  | query | true |string  |    |
|type| 类型(0市价1限价),可用值:0,1  | query | true |string  |    |

**响应示例**:

```json
{
	"code": "",
	"data": "",
	"description": ""
}
```

**响应参数**:


| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
|code| 响应代码  |string  |    |
|data| 响应数据  |string  |    |
|description| 响应描述  |string  |    |


# account

## 获取账户余额


**接口描述**:


**接口地址**:`/openapi/v1/capital/balance`


**请求方式**：`GET`


**consumes**:``


**produces**:`["application/xml","application/json"]`



**请求参数**：

| 参数名称         | 参数说明     |     in |  是否必须      |  数据类型  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |

**响应示例**:

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

**响应参数**:


| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
|code| 响应代码  |string  |    |
|data| 响应数据  |array  | 用户资金信息   |
|description| 响应描述  |string  |    |



**schema属性说明**




**用户资金信息**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
|availableAmount | 可用余额   |number  |    |
|currency | 币种名   |string  |    |
|frozenAmount | 冻结金额   |number  |    |


## 获取充币地址


**接口描述**:


**接口地址**:`/openapi/v1/capital/depositAddress`


**请求方式**：`GET`


**consumes**:``


**produces**:`["application/json"]`



**请求参数**：

| 参数名称         | 参数说明     |     in |  是否必须      |  数据类型  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|currencyName| 币种名称  | query | true |string  |    |

**响应示例**:

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

**响应参数**:


| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
|code| 响应代码  |string  |    |
|data| 响应数据  |获取充币地址  | 获取充币地址   |
|description| 响应描述  |string  |    |



**schema属性说明**




**获取充币地址**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
|account | 带tag标签的币种的统一指定地址   |string  |    |
|address | 账户收币地址   |string  |    |
|havaTag | 是否拥有标签地址   |string  |    |


## 获取充值记录


**接口描述**:


**接口地址**:`/openapi/v1/capital/depositRecord`


**请求方式**：`GET`



**请求参数**：

| 参数名称         | 参数说明     |     in |  是否必须      |  数据类型  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|pageNo| 当前页数  | query | false |integer  |    |
|pageSize| 每页显示条数  | query | false |integer  |    |

**响应示例**:

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

**响应参数**:


| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
|code| 响应代码  |string  |    |
|data| 响应数据  |PageInfo«充值记录信息»  | PageInfo«充值记录信息»   |
|description| 响应描述  |string  |    |



**schema属性说明**




**PageInfo«充值记录信息»**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
|endRow |    |integer(int32)  |    |
|firstPage |    |integer(int32)  |    |
|hasNextPage |    |boolean  |    |
|hasPreviousPage |    |boolean  |    |
|isFirstPage |    |boolean  |    |
|isLastPage |    |boolean  |    |
|lastPage |    |integer(int32)  |    |
|list |    |array  | 充值记录信息   |
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

**充值记录信息**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
|accountAddress | 收币地址   |string  |    |
|currency | 转入币种   |string  |    |
|dateReceive | 转入时间   |string(date-time)  |    |
|id | ID   |string  |    |
|receiveAmount | 转入币数量   |number  |    |
|serialNumber | 订单流水号(充币交易id)   |string  |    |
|state | 状态：3表示正在进行    1表示已完成   |string  |    |


## 提币申请


**接口描述**:


**接口地址**:`/openapi/v1/capital/withdraw`


**请求方式**：`POST`


**consumes**:`["application/json"]`


**produces**:`["application/xml","application/json"]`



**请求参数**：

| 参数名称         | 参数说明     |     in |  是否必须      |  数据类型  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|address| 提币地址  | query | true |string  |    |
|currency| 币种名  | query | true |string  |    |
|tag| 标签值  | query | true |string  |    |
|widhdrawAmt| 提币数量  | query | true |string  |    |

**响应示例**:

```json
{
	"code": "",
	"data": {},
	"description": ""
}
```

**响应参数**:


| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
|code| 响应代码  |string  |    |
|data| 响应数据  |object  |    |
|description| 响应描述  |string  |    |






## 获取提币记录


**接口描述**:


**接口地址**:`/openapi/v1/capital/withdrawRecord`


**请求方式**：`GET`


**请求参数**：

| 参数名称         | 参数说明     |     in |  是否必须      |  数据类型  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|pageNo| 当前页数  | query | false |integer  |    |
|pageSize| 每页显示条数  | query | false |integer  |    |

**响应示例**:

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

**响应参数**:


| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
|code| 响应代码  |string  |    |
|data| 响应数据  |PageInfo«提币记录信息»  | PageInfo«提币记录信息»   |
|description| 响应描述  |string  |    |



**schema属性说明**




**PageInfo«提币记录信息»**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
|endRow |    |integer(int32)  |    |
|firstPage |    |integer(int32)  |    |
|hasNextPage |    |boolean  |    |
|hasPreviousPage |    |boolean  |    |
|isFirstPage |    |boolean  |    |
|isLastPage |    |boolean  |    |
|lastPage |    |integer(int32)  |    |
|list |    |array  | 提币记录信息   |
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

**提币记录信息**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
|accountAddress | 转币地址   |string  |    |
|actualAmount | 实到金额数量   |number  |    |
|applyStatus | 申请状态 1:待审核2:审核通过3:审核不通过   |string  |    |
|checkAddress | 币种区块浏览地址   |string  |    |
|currencyName | 币种名称   |string  |    |
|dateCreate | 申请时间   |string(date-time)  |    |
|id | 主键id   |string  |    |
|poundage | 手续费   |number  |    |
|tag | tag值   |string  |    |
|txId | 第三方依据流水   |string  |    |
|withdrawAmount | 转币数量   |number  |    |




# transaction

## 查询法币配置信息

**接口地址** `/openapi/v1/transaction/legalConf`


**请求方式** `GET`


**请求参数**

暂无



**响应参数**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
| code     |响应代码      |    string   |       |
| data     |响应数据      |    array   |   法币币种信息    |
| description     |响应描述      |    string   |       |
            



**schema属性说明**
  
**法币币种信息**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
| createAt         |     创建时间      |  integer(int64)   |      |
| currencyId         |     稳定币ID      |  string   |      |
| currencyName         |     稳定币名称      |  string   |      |
| exportChannelRate         |     汇出通道费率      |  number   |      |
| exportExcRate         |     汇出汇率      |  number   |      |
| exportMaxAmount         |     汇出单笔最大值      |  number   |      |
| exportMinAmount         |     汇出单笔最小值      |  number   |      |
| exportStatus         |     汇出状态: 1.启用; 2.停用;      |  string   |      |
| id         |     法币ID      |  string   |      |
| importChannelRate         |     汇入通道费率      |  number   |      |
| importExcRate         |     汇入汇率      |  number   |      |
| importMaxAmount         |     汇入单笔最大值      |  number   |      |
| importMinAmount         |     汇入单笔最小值      |  number   |      |
| importStatus         |     汇入状态: 1.启用; 2.停用;      |  string   |      |
| logoUrl         |     logo图片url      |  string   |      |
| name         |     法币名称      |  string   |      |
| projectName         |     项目名      |  string   |      |
            




**响应示例**


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


## 汇入

**接口地址** `/openapi/v1/transaction/in`


**请求方式** `POST`


**接口描述** 


**请求参数**

| 参数名称         | 参数说明     |     请求类型 |  是否必须      |  数据类型   |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
| legalAmount         |      法币数量   |     query        |       true      | number   |      |
| legalCurrenyId         |      法币ID   |     query        |       true      | string   |      |



**响应参数**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
| code     |响应代码      |    string   |       |
| data     |响应数据      |    交易申请信息   |   交易申请信息    |
| description     |响应描述      |    string   |       |
            

**schema属性说明**
  
**交易申请信息**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
| bankSerialNumber         |     银行流水号      |  string   |      |
| channelFee         |     收取的通道费      |  number   |      |
| channelFeeRate         |     通道费率      |  number   |      |
| createAt         |     创建时间      |  integer(int64)   |      |
| currencyAmount         |     稳定币数量      |  number   |      |
| currencyId         |     稳定币ID      |  string   |      |
| currenyName         |     稳定币名称      |  string   |      |
| exchRate         |     当前实时汇率      |  number   |      |
| fee         |     手续费（收取法币手续费）      |  number   |      |
| id         |     主键ID      |  string   |      |
| legalAmount         |     法币数量      |  number   |      |
| legalCurrenyId         |     法币ID      |  string   |      |
| legalCurrenyName         |     法币名称      |  string   |      |
| noteCode         |     转账汇款备注码      |  string   |      |
| originalCurrencyAmount         |     原稳定币数量      |  number   |      |
| payAt         |     付款时间      |  integer(int64)   |      |
| payBirthDate         |     汇款人出生日期(yyyy-MM-dd)      |  string   |      |
| payCountry         |     汇款人国籍      |  string   |      |
| payDeadline         |     付款截止时间      |  integer(int64)   |      |
| payFirstName         |     汇款人名字      |  string   |      |
| payLastName         |     汇款人姓氏      |  string   |      |
| payMiddleName         |     汇款人中间名      |  string   |      |
| payType         |     支付方式 1.微信 2.支付宝 3.银行卡      |  string   |      |
| receiveAccount         |     平台收款账户      |  平台收款账户   | 平台收款账户     |
| receiveId         |     收款账户ID      |  string   |      |
| remark         |     备注      |  string   |      |
| source         |     来源: 1.PC 3.安卓 4.苹果 5.微信 6.H5      |  string   |      |
| status         |     状态: 1.待付款 2.支付超时 3.已取消 4.待审核 5.审核不通过 6.已完结      |  string   |      |
| transactionType         |     交易类型: 1.汇入; 2.汇出;      |  string   |      |
| userCode         |     UID用户编号      |  string   |      |
| userId         |     用户Id      |  string   |      |
| verifiedAt         |     审核时间      |  integer(int64)   |      |
| verifiedDescCn         |     审核描述(中文)      |  string   |      |
| verifiedDescEs         |     审核描述(英文)      |  string   |      |
            

**平台收款账户**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
| address         |     收款人地址      |  string   |      |
| bankAddress         |     收款银行地址      |  string   |      |
| bankCardNo         |     收款银行账号      |  string   |      |
| bankCity         |     收款银行城市      |  string   |      |
| bankCountry         |     收款银行国家      |  string   |      |
| bankName         |     收款银行名称      |  string   |      |
| bankProvince         |     收款银行省份      |  string   |      |
| bankSwiftCode         |     收款银行Swift码      |  string   |      |
| city         |     收款人城市      |  string   |      |
| country         |     收款人国家      |  string   |      |
| createAt         |     创建时间      |  integer(int64)   |      |
| firstName         |     收款人名字      |  string   |      |
| id         |     主键ID      |  string   |      |
| lastModifyAt         |     最后修改时间      |  integer(int64)   |      |
| lastName         |     收款人姓氏      |  string   |      |
| middleName         |     收款人中间名      |  string   |      |
| province         |     收款人省份      |  string   |      |
| remittanceType         |     转账汇款方式：1.PH Local; 2.Swift      |  string   |      |
| symbol         |     资产类型(目前仅支持USD和PHP)      |  string   |      |
| type         |     账户类型: 1. 系统账户; 2.平台用户;      |  string   |      |
| userId         |     用户ID      |  string   |      |
            

**响应示例**


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


## 汇出

**接口地址** `/openapi/v1/transaction/out`


**请求方式** `POST`



**接口描述** 

**请求参数**

| 参数名称         | 参数说明     |     请求类型 |  是否必须      |  数据类型   |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
| address         |      收款人地址   |     query        |       true      | string   |      |
| bankAddress         |      收款银行地址   |     query        |       false      | string   |      |
| bankCardNo         |      收款银行账号   |     query        |       true      | string   |      |
| bankCity         |      收款银行城市   |     query        |       false      | string   |      |
| bankCountry         |      收款银行国家   |     query        |       false      | string   |      |
| bankName         |      收款银行名称   |     query        |       true      | string   |      |
| bankProvince         |      收款银行省份   |     query        |       false      | string   |      |
| bankSwiftCode         |      收款银行Swift码   |     query        |       false      | string   |      |
| city         |      收款人城市   |     query        |       true      | string   |      |
| country         |      收款人国家   |     query        |       true      | string   |      |
| currencyAmount         |      稳定币数量   |     query        |       false      | number   |      |
| firstName         |      收款人名字   |     query        |       true      | string   |      |
| lastName         |      收款人姓氏   |     query        |       true      | string   |      |
| legalCurrenyId         |      法币ID   |     query        |       false      | string   |      |
| locale         |      语言   |     query        |       false      | string   |      |
| middleName         |      收款人中间名   |     query        |       false      | string   |      |
| province         |      收款人省份   |     query        |       true      | string   |      |
| tradePwd         |      交易密码   |     query        |       false      | string   |      |
| type         |      账户类型: 2.平台用户   |     query        |       false      | string   |      |
| symbol         |      法币类型 目前仅支持USD和PHP   |     query        |       false      | string   |      |
| remittanceType         |      转账汇款方式：1.PH Local; 2.Swift  |     query        |       false      | string   |      |
            


**响应参数**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
| code     |响应代码      |    string   |       |
| data     |响应数据      |    交易申请信息   |   交易申请信息    |
| description     |响应描述      |    string   |       |




**schema属性说明**
  
**交易申请信息**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
| bankSerialNumber         |     银行流水号      |  string   |      |
| channelFee         |     收取的通道费      |  number   |      |
| channelFeeRate         |     通道费率      |  number   |      |
| createAt         |     创建时间      |  integer(int64)   |      |
| currencyAmount         |     稳定币数量      |  number   |      |
| currencyId         |     稳定币ID      |  string   |      |
| currenyName         |     稳定币名称      |  string   |      |
| exchRate         |     当前实时汇率      |  number   |      |
| fee         |     手续费（收取法币手续费）      |  number   |      |
| id         |     主键ID      |  string   |      |
| legalAmount         |     法币数量      |  number   |      |
| legalCurrenyId         |     法币ID      |  string   |      |
| legalCurrenyName         |     法币名称      |  string   |      |
| noteCode         |     转账汇款备注码      |  string   |      |
| originalCurrencyAmount         |     原稳定币数量      |  number   |      |
| payAt         |     付款时间      |  integer(int64)   |      |
| payBirthDate         |     汇款人出生日期(yyyy-MM-dd)      |  string   |      |
| payCountry         |     汇款人国籍      |  string   |      |
| payDeadline         |     付款截止时间      |  integer(int64)   |      |
| payFirstName         |     汇款人名字      |  string   |      |
| payLastName         |     汇款人姓氏      |  string   |      |
| payMiddleName         |     汇款人中间名      |  string   |      |
| payType         |     支付方式 1.微信 2.支付宝 3.银行卡      |  string   |      |
| receiveAccount         |     平台收款账户      |  平台收款账户   | 平台收款账户     |
| receiveId         |     收款账户ID      |  string   |      |
| remark         |     备注      |  string   |      |
| source         |     来源: 1.PC 3.安卓 4.苹果 5.微信 6.H5      |  string   |      |
| status         |     状态: 1.待付款 2.支付超时 3.已取消 4.待审核 5.审核不通过 6.已完结      |  string   |      |
| transactionType         |     交易类型: 1.汇入; 2.汇出;      |  string   |      |
| userCode         |     UID用户编号      |  string   |      |
| userId         |     用户Id      |  string   |      |
| verifiedAt         |     审核时间      |  integer(int64)   |      |
| verifiedDescCn         |     审核描述(中文)      |  string   |      |
| verifiedDescEs         |     审核描述(英文)      |  string   |      |
            

**平台收款账户**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
| address         |     收款人地址      |  string   |      |
| bankAddress         |     收款银行地址      |  string   |      |
| bankCardNo         |     收款银行账号      |  string   |      |
| bankCity         |     收款银行城市      |  string   |      |
| bankCountry         |     收款银行国家      |  string   |      |
| bankName         |     收款银行名称      |  string   |      |
| bankProvince         |     收款银行省份      |  string   |      |
| bankSwiftCode         |     收款银行Swift码      |  string   |      |
| city         |     收款人城市      |  string   |      |
| country         |     收款人国家      |  string   |      |
| createAt         |     创建时间      |  integer(int64)   |      |
| firstName         |     收款人名字      |  string   |      |
| id         |     主键ID      |  string   |      |
| lastModifyAt         |     最后修改时间      |  integer(int64)   |      |
| lastName         |     收款人姓氏      |  string   |      |
| middleName         |     收款人中间名      |  string   |      |
| province         |     收款人省份      |  string   |      |
| remittanceType         |     转账汇款方式：1.PH Local; 2.Swift      |  string   |      |
| symbol         |     资产类型(目前仅支持USD和PHP)      |  string   |      |
| type         |     账户类型: 1. 系统账户; 2.平台用户;      |  string   |      |
| userId         |     用户ID      |  string   |      |
            




**响应示例**


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


## 撤销

**接口地址** `/openapi/v1/transaction/cancel`


**请求方式** `POST`


**接口描述** 

**请求参数**

| 参数名称         | 参数说明     |     请求类型 |  是否必须      |  数据类型   |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
| id         |      主键ID   |     query        |       true      | string   |      |       



**响应参数**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
| code     |响应代码      |    string   |       |
| data     |响应数据      |    object   |       |
| description     |响应描述      |    string   |       |





**响应示例**


```json
{
	"code": "",
	"data": {},
	"description": ""
}
```


## 已付款

**接口地址** `/openapi/v1/transaction/pay`


**请求方式** `POST`


**接口描述** 

**请求参数**

| 参数名称         | 参数说明     |     请求类型 |  是否必须      |  数据类型   |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
| apiKey         |      apiKey   |     header        |       true      | string   |      |
| id         |      主键ID   |     query        |       true      | string   |      |


**响应参数**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
| code     |响应代码      |    string   |       |
| data     |响应数据      |    object   |       |
| description     |响应描述      |    string   |       |
            

**响应示例**


```json
{
	"code": "",
	"data": null,
	"description": ""
}
```


## 查询交易(汇入、汇出)记录

**接口地址** `/openapi/v1/transaction/transactionList`


**请求方式** `POST`




**接口描述** 

**请求参数**

| 参数名称         | 参数说明     |     请求类型 |  是否必须      |  数据类型   |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
| pageNo         |      当前页数   |     query        |       false      | integer   |      |
| pageSize         |      每页显示条数   |     query        |       false      | integer   |      |
| statuses         |      状态: 1.待付款 2.支付超时 3.已取消 4.待审核 5.审核不通过 6.已完结   |     query        |       false      | array   | string     |
            


**响应参数**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
| code     |响应代码      |    string   |       |
| data     |响应数据      |    PageInfo«交易申请信息»   |   PageInfo«交易申请信息»    |
| description     |响应描述      |    string   |       |
            



**schema属性说明**
  
**PageInfo«交易申请信息»**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
| endRow         |           |  integer(int32)   |      |
| firstPage         |           |  integer(int32)   |      |
| hasNextPage         |           |  boolean   |      |
| hasPreviousPage         |           |  boolean   |      |
| isFirstPage         |           |  boolean   |      |
| isLastPage         |           |  boolean   |      |
| lastPage         |           |  integer(int32)   |      |
| list         |           |  array   | 交易申请信息     |
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


**交易申请信息**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
| bankSerialNumber         |     银行流水号      |  string   |      |
| channelFee         |     收取的通道费      |  number   |      |
| channelFeeRate         |     通道费率      |  number   |      |
| createAt         |     创建时间      |  integer(int64)   |      |
| currencyAmount         |     稳定币数量      |  number   |      |
| currencyId         |     稳定币ID      |  string   |      |
| currenyName         |     稳定币名称      |  string   |      |
| exchRate         |     当前实时汇率      |  number   |      |
| fee         |     手续费（收取法币手续费）      |  number   |      |
| id         |     主键ID      |  string   |      |
| legalAmount         |     法币数量      |  number   |      |
| legalCurrenyId         |     法币ID      |  string   |      |
| legalCurrenyName         |     法币名称      |  string   |      |
| noteCode         |     转账汇款备注码      |  string   |      |
| originalCurrencyAmount         |     原稳定币数量      |  number   |      |
| payAt         |     付款时间      |  integer(int64)   |      |
| payBirthDate         |     汇款人出生日期(yyyy-MM-dd)      |  string   |      |
| payCountry         |     汇款人国籍      |  string   |      |
| payDeadline         |     付款截止时间      |  integer(int64)   |      |
| payFirstName         |     汇款人名字      |  string   |      |
| payLastName         |     汇款人姓氏      |  string   |      |
| payMiddleName         |     汇款人中间名      |  string   |      |
| payType         |     支付方式 1.微信 2.支付宝 3.银行卡      |  string   |      |
| receiveAccount         |     平台收款账户      |  平台收款账户   | 平台收款账户     |
| receiveId         |     收款账户ID      |  string   |      |
| remark         |     备注      |  string   |      |
| source         |     来源: 1.PC 3.安卓 4.苹果 5.微信 6.H5      |  string   |      |
| status         |     状态: 1.待付款 2.支付超时 3.已取消 4.待审核 5.审核不通过 6.已完结      |  string   |      |
| transactionType         |     交易类型: 1.汇入; 2.汇出;      |  string   |      |
| userCode         |     UID用户编号      |  string   |      |
| userId         |     用户Id      |  string   |      |
| verifiedAt         |     审核时间      |  integer(int64)   |      |
| verifiedDescCn         |     审核描述(中文)      |  string   |      |
| verifiedDescEs         |     审核描述(英文)      |  string   |      |
            

**平台收款账户**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
| address         |     收款人地址      |  string   |      |
| bankAddress         |     收款银行地址      |  string   |      |
| bankCardNo         |     收款银行账号      |  string   |      |
| bankCity         |     收款银行城市      |  string   |      |
| bankCountry         |     收款银行国家      |  string   |      |
| bankName         |     收款银行名称      |  string   |      |
| bankProvince         |     收款银行省份      |  string   |      |
| bankSwiftCode         |     收款银行Swift码      |  string   |      |
| city         |     收款人城市      |  string   |      |
| country         |     收款人国家      |  string   |      |
| createAt         |     创建时间      |  integer(int64)   |      |
| firstName         |     收款人名字      |  string   |      |
| id         |     主键ID      |  string   |      |
| lastModifyAt         |     最后修改时间      |  integer(int64)   |      |
| lastName         |     收款人姓氏      |  string   |      |
| middleName         |     收款人中间名      |  string   |      |
| province         |     收款人省份      |  string   |      |
| remittanceType         |     转账汇款方式：1.PH Local; 2.Swift      |  string   |      |
| symbol         |     资产类型(目前仅支持USD和PHP)      |  string   |      |
| type         |     账户类型: 1. 系统账户; 2.平台用户;      |  string   |      |
| userId         |     用户ID      |  string   |      |
            




**响应示例**


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


