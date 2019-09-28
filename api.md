**GOW RESTful API**




# API简介

欢迎使用gow API！ 您可以使用此 API 获得市场行情数据，进行交易，并且管理你的账户。


# 接入说明

## 接入url

**REST API**:http://47.75.162.18:56666

## 请求头部参数信息

接口请求头部必须包含以下信息

* content-type：application/json
* timestamp：请求时间戳，单位毫秒
* apiKey：API KEY访问密钥
* sign：签名信息


## 签名认证

### 创建API KEY

API Key 包括以下两部分
* API KEY api访问密钥
* Secret Key 签名认证加密所使用的密钥（仅申请时可见）

### 签名步骤

签名使用HmacSHA512算法签名，签名内容将各参数使用字符 “&” 连接

#### 签名内容

**GET请求**:只需要将apiKey和timestamp按照ASCII码的顺序对参数名进行倒序排序，如：
* timestamp=1566322200000&apiKey=4565B83XXXXXXXXXXXXF123

**POST请求**:需将apiKey和timestamp以及对应接口传参按照ASCII码的顺序对参数名进行倒序排序，如撤销订单：
* timestamp=1566322200000&orderId=E12345XXXXXXXX&apiKey=4565B83XXXXXXXXXXXXF123

#### 签名

将生成的签名内容和secretKey使用HmacSHA512算法生成签名

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

## 请求格式

所有的API请求都以GET或者POST形式发出。对于GET请求，所有的参数都在路径参数里；对于POST请求，所有参数则以JSON格式发送在请求主体（body）里，头部信息（header）中
必须传timestamp、apiKey、sign

## 返回内容格式

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
|code| 响应代码  |string  |  返回000000为调用成功，其他code均为错误代码  |
|data| 响应数据  |Object  |    |
|description| 响应描述  |string  |    |


# common

## 获取基础币种


**接口描述**:


**接口地址**:`/openapi/v1/common/currencys`


**请求方式**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**请求参数**：
暂无



**响应示例**:

```json
{
	"code": "",
	"data": [],
	"description": ""
}
```

**响应参数**:


| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
|code| 响应代码  |string  |    |
|data| 币种列表  |array  |    |
|description| 响应描述  |string  |    |






## 获取某交易对详情


**接口描述**:


**接口地址**:`/openapi/v1/common/symbolInfo`


**请求方式**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**请求参数**：

| 参数名称         | 参数说明     |     in |  是否必须      |  数据类型  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|symbol| 交易对  | query | true |string  |    |

**响应示例**:

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

**响应参数**:


| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
|code| 响应代码  |string  |    |
|data| 响应数据  |ExchangeCoin  | ExchangeCoin   |
|description| 响应描述  |string  |    |



**schema属性说明**




**ExchangeCoin**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
|baseCoinScale | 基币小数精度   |integer(int32)  |    |
|baseSymbol | 结算币种符号   |string  |    |
|buyPriceLimit | 买入价格幅度限制   |number  |    |
|coinScale | 交易币小数精度   |integer(int32)  |    |
|coinSymbol | 交易币种符号   |string  |    |
|enable | 状态，1：启用，2：禁止   |integer(int32)  |    |
|enableMarketBuy | 是否启用市价买,可用值:0,1   |string  |    |
|enableMarketSell | 是否启用市价卖,可用值:0,1   |string  |    |
|fee | 交易手续费   |number  |    |
|flag | 标签位，用于推荐，排序等,默认为0，1表示推荐   |integer(int32)  |    |
|maxTradingOrder | 最大允许同时交易的订单数，0表示不限制   |integer(int32)  |    |
|maxTradingTime | 最大交易时间   |integer(int32)  |    |
|maxVolume | 最大下单量，0表示不限制   |number  |    |
|minSellPrice | 卖单最低价格   |number  |    |
|minTurnover | 最小成交额   |number  |    |
|minVolume | 最小下单量，0表示不限制   |number  |    |
|sellPriceLimit | 卖出价格幅度限制   |number  |    |
|sort | 排序   |integer(int32)  |    |
|symbol | 交易对   |string  |    |
|zone | 交易区域   |integer(int32)  |    |



## 获取支持的交易对


**接口描述**:


**接口地址**:`/openapi/v1/common/symbols`


**请求方式**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**请求参数**：
暂无



**响应示例**:

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

**响应参数**:


| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
|code| 响应代码  |string  |    |
|data| 响应数据  |array  | ExchangeCoin   |
|description| 响应描述  |string  |    |



**schema属性说明**




**ExchangeCoin**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
|baseCoinScale | 基币小数精度   |integer(int32)  |    |
|baseSymbol | 结算币种符号   |string  |    |
|buyPriceLimit | 买入价格幅度限制   |number  |    |
|coinScale | 交易币小数精度   |integer(int32)  |    |
|coinSymbol | 交易币种符号   |string  |    |
|enable | 状态，1：启用，2：禁止   |integer(int32)  |    |
|enableMarketBuy | 是否启用市价买,可用值:0,1   |string  |    |
|enableMarketSell | 是否启用市价卖,可用值:0,1   |string  |    |
|fee | 交易手续费   |number  |    |
|flag | 标签位，用于推荐，排序等,默认为0，1表示推荐   |integer(int32)  |    |
|maxTradingOrder | 最大允许同时交易的订单数，0表示不限制   |integer(int32)  |    |
|maxTradingTime | 最大交易时间   |integer(int32)  |    |
|maxVolume | 最大下单量，0表示不限制   |number  |    |
|minSellPrice | 卖单最低价格   |number  |    |
|minTurnover | 最小成交额   |number  |    |
|minVolume | 最小下单量，0表示不限制   |number  |    |
|sellPriceLimit | 卖出价格幅度限制   |number  |    |
|sort | 排序   |integer(int32)  |    |
|symbol | 交易对   |string  |    |
|zone | 交易区域   |integer(int32)  |    |


# market

## 查询盘口(深度)数据


**接口描述**:


**接口地址**:`/openapi/v1/market/exchangePlate`


**请求方式**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**请求参数**：

| 参数名称         | 参数说明     |     in |  是否必须      |  数据类型  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|symbol| 交易对  | query | true |string  |    |

**响应示例**:

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

**响应参数**:


| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
|code| 响应代码  |string  |    |
|data| 响应数据  |array  | TradePlateItem   |
|description| 响应描述  |string  |    |



**schema属性说明**




**TradePlateItem**

| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | ------------------|--------|----------- |
|amount | 数量   |number  |    |
|changed |    |boolean  |    |
|price | 价格   |number  |    |

## 获取币种历史K线


**接口描述**:


**接口地址**:`/openapi/v1/market/history`


**请求方式**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**请求参数**：

| 参数名称         | 参数说明     |     in |  是否必须      |  数据类型  |  schema  |
| ------------ | -------------------------------- |-----------|--------|----|--- |
|from| 开始时间戳  | query | true |integer  |    |
|resolution| K线周期(1,15,30,60,240,D,W,M)  | query | true |string  |    |
|symbol| 交易对  | query | true |string  |    |
|to| 结束时间戳  | query | true |integer  |    |

**响应示例**:

```json
{
	"code": "",
	"data": [],
	"description": ""
}
```

**响应参数**:


| 参数名称         | 参数说明                             |    类型 |  schema |
| ------------ | -------------------|-------|----------- |
|code| 响应代码  |string  |    |
|data| 响应数据（按顺序为：时间戳、开盘价、最高价、最低价、收盘价、交易额）  |array  |    |
|description| 响应描述  |string  |    |



## 查询最近成交记录


**接口描述**:


**接口地址**:`/openapi/v1/market/latestTrade`


**请求方式**：`GET`


**consumes**:``


**produces**:`["*/*","application/json"]`



**请求参数**：

| 参数名称         | 参数说明     |     in |  是否必须      |  数据类型  |  schema  |
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


