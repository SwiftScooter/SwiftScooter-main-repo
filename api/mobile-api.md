---
title: 个人项目
language_tabs:
  - shell: Shell
  - http: HTTP
  - javascript: JavaScript
  - ruby: Ruby
  - python: Python
  - php: PHP
  - java: Java
  - go: Go
toc_footers: []
includes: []
search: true
code_clipboard: true
highlight_theme: darkula
headingLevel: 2
generator: "@tarslib/widdershins v4.0.29"

---

# 个人项目

Base URLs:

# Authentication

- HTTP Authentication, scheme: bearer

# 用户端

## POST 用户登录

POST /user/login

输入邮箱密码来进行用户登录，仅返回token。（查询用户信息已迁移至单独接口）

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|email|query|string| 是 |none|
|password|query|string| 是 |none|

> 返回示例

> 200 Response

```json
{
  "token": "string"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

*用户信息*

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» token|string|true|none|用户令牌|none|

## GET 获取用户信息

GET /user/current

获取当前用户信息。注意用户组要结合过期时间一起检查。

> 返回示例

> 200 Response

```json
{
  "userId": 0,
  "email": "string",
  "userName": "string",
  "phoneNumber": "string",
  "userGroup": "common",
  "expirationTime": "string",
  "cardNumber": "string"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

*用户信息*

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» userId|integer|true|none|用户ID|none|
|» email|string|true|none|用户邮箱|none|
|» userName|string|true|none|用户名|none|
|» phoneNumber|string|true|none|联系电话|none|
|» userGroup|string|true|none|所处分组|none|
|» expirationTime|string|true|none|分组过期时间|none|
|» cardNumber|string|true|none|信用卡卡号|none|

#### 枚举值

|属性|值|
|---|---|
|userGroup|common|
|userGroup|student|
|userGroup|senior|

## GET 获取所有站点和车

GET /user/stations-scooters

> 返回示例

> 200 Response

```json
{
  "station": [
    {
      "stationId": 0,
      "name": "string",
      "longitude": 0,
      "latitude": 0,
      "scooters": [
        {
          "scooterId": 0,
          "longitude": 0,
          "latitude": 0,
          "type": "X1 City Rider",
          "battery": 0,
          "status": "available",
          "stationId": 0,
          "price": 0
        }
      ]
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

*用户数据*

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» station|[object]|true|none||none|
|»» stationId|integer|true|none||站点id|
|»» name|string|true|none||none|
|»» longitude|number|true|none||经度|
|»» latitude|number|true|none||纬度|
|»» scooters|[object]|true|none||站点的车的集合|
|»»» scooterId|integer|true|none||车id|
|»»» longitude|number|true|none||经度|
|»»» latitude|number|true|none||纬度|
|»»» type|string|true|none||型号|
|»»» battery|number|true|none||电量（0.83）|
|»»» status|string|true|none||none|
|»»» stationId|integer|true|none||所属站点的id|
|»»» price|number|true|none||新增！滑板车单价|

#### 枚举值

|属性|值|
|---|---|
|type|X1 City Rider|
|type|E2 Pro Cruiser|
|type|S3 Speedster|
|type|L4 FlexMove|
|status|available|
|status|unavailable|
|status|maintenance|
|status|in_use|
|status|deleted|

## GET 获取指定站点信息（包含滑板车）

GET /user/station/{stationId}

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|stationId|path|string| 是 |none|

> 返回示例

> 200 Response

```json
{
  "stationId": 0,
  "name": "string",
  "longitude": 0,
  "latitude": 0,
  "scooters": [
    {
      "scooterId": 0,
      "longitude": 0,
      "latitude": 0,
      "type": "X1 City Rider",
      "battery": 0,
      "status": "available",
      "stationId": 0,
      "price": 0
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

*用户数据*

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» stationId|integer|true|none||站点id|
|» name|string|true|none||none|
|» longitude|number|true|none||经度|
|» latitude|number|true|none||纬度|
|» scooters|[object]|true|none||none|
|»» scooterId|integer|true|none||车id|
|»» longitude|number|true|none||经度|
|»» latitude|number|true|none||纬度|
|»» type|string|true|none||型号|
|»» battery|number|true|none||电量（0.83）|
|»» status|string|true|none||none|
|»» stationId|integer|true|none||所属站点的id|
|»» price|number|true|none|滑板车单价|none|

#### 枚举值

|属性|值|
|---|---|
|type|X1 City Rider|
|type|E2 Pro Cruiser|
|type|S3 Speedster|
|type|L4 FlexMove|
|status|available|
|status|unavailable|
|status|maintenance|
|status|in_use|
|status|deleted|

## GET 获取反馈列表

GET /user/feedbacks

获取所有的反馈

> 返回示例

> 200 Response

```json
{
  "feedbacks": [
    {
      "feedbackId": 0,
      "orderId": 0,
      "region": "string",
      "description": "string",
      "priority": "string",
      "status": "submitted",
      "createTime": "string",
      "updateTime": "string",
      "scooter": {
        "scooterId": 0,
        "longitude": 0,
        "latitude": 0,
        "type": "X1 City Rider",
        "battery": 0,
        "status": "available",
        "stationId": 0
      }
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» feedbacks|[object]|true|none||none|
|»» feedbackId|integer|true|none||none|
|»» orderId|integer|true|none||none|
|»» region|string|true|none||none|
|»» description|string|true|none||none|
|»» priority|string|true|none||none|
|»» status|string|true|none||状态|
|»» createTime|string|true|none||none|
|»» updateTime|string|true|none||none|
|»» scooter|object|true|none||none|
|»»» scooterId|integer|true|none||车id|
|»»» longitude|number|true|none||经度|
|»»» latitude|number|true|none||纬度|
|»»» type|string|true|none||型号|
|»»» battery|number|true|none||电量（0.83）|
|»»» status|string|true|none||none|
|»»» stationId|integer|true|none||所属站点的id|

#### 枚举值

|属性|值|
|---|---|
|status|submitted|
|status|processing|
|status|resolved|
|status|closed|
|type|X1 City Rider|
|type|E2 Pro Cruiser|
|type|S3 Speedster|
|type|L4 FlexMove|
|status|available|
|status|unavailable|
|status|maintenance|
|status|in_use|
|status|deleted|

## GET 获取指定滑板车信息

GET /user/scooter/{scooterId}

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|scooterId|path|integer| 是 |none|

> 返回示例

> 200 Response

```json
{
  "scooterId": 0,
  "longitude": 0,
  "latitude": 0,
  "type": "X1 City Rider",
  "battery": 0,
  "status": "available",
  "stationId": 0,
  "price": 0
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

*用户数据*

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» scooterId|integer|true|none||车id|
|» longitude|number|true|none||经度|
|» latitude|number|true|none||纬度|
|» type|string|true|none||型号|
|» battery|number|true|none||电量（0.83）|
|» status|string|true|none||none|
|» stationId|integer|true|none||所属站点的id|
|» price|number|true|none||none|

#### 枚举值

|属性|值|
|---|---|
|type|X1 City Rider|
|type|E2 Pro Cruiser|
|type|S3 Speedster|
|type|L4 FlexMove|
|status|available|
|status|unavailable|
|status|maintenance|
|status|in_use|
|status|deleted|

## GET 获取站点列表

GET /user/stations

> 返回示例

> 200 Response

```json
{
  "station": [
    {
      "stationId": 0,
      "name": "string",
      "longitude": 0,
      "latitude": 0
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

*用户数据*

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» station|[[station](#schemastation)]|true|none||none|
|»» stationId|integer|true|none||站点id|
|»» name|string|true|none||none|
|»» longitude|number|true|none||经度|
|»» latitude|number|true|none||纬度|

## GET 预览订单（预定过程中）

GET /user/preview-order

预定过程中实时请求价格，优惠策略等。

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|scooterId|query|integer| 否 |none|
|timePeriod|query|integer| 否 |none|

> 返回示例

> 200 Response

```json
{
  "cardNumber": "string",
  "scooterPrice": 0,
  "originalPrice": 0,
  "discounts": [
    {
      "discountId": 0,
      "type": "string",
      "num": 0,
      "name": "string"
    }
  ],
  "rentalPrice": 0
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» cardNumber|string|false|none||信用卡卡号（可选、如果绑定了）|
|» scooterPrice|number|true|none||滑板车的单价|
|» originalPrice|number|true|none||预计原价|
|» discounts|[[discount](#schemadiscount)]|true|none||[命中的折扣]|
|»» discountId|integer|true|none||优惠id|
|»» type|string|true|none||优惠的类型|
|»» num|number|true|none||优惠的数额|
|»» name|string|true|none||命中优惠的名字|
|» rentalPrice|number|true|none||none|

## POST 注册

POST /user/register

注意：注册现在要求《必须》填入手机号，不得缺省。用户登录仍然使用邮箱和密码，但是在注册流程中会要求用户输入手机号和用户名。

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|email|query|string| 是 |邮箱|
|password|query|string| 是 |密码|
|userName|query|string| 是 |用户名|
|phoneNumber|query|string| 否 |none|

> 返回示例

> 200 Response

```json
{
  "message": "string"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» message|string|true|none||none|

状态码 **400**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||none|
|» message|string|true|none||none|

## POST 租车请求

POST /user/order/create

后端计算价格

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|scooterId|query|integer| 否 |目标车id|
|startTime|query|string| 否 |起始时间|
|timePeriod|query|integer| 否 |租赁时长（分钟）|

> 返回示例

> 200 Response

```json
{
  "orderId": 0,
  "scooter": {
    "scooterId": 0,
    "type": "X1 City Rider",
    "status": "available",
    "stationId": 0
  },
  "station": {
    "stationId": 0,
    "name": "string",
    "longitude": 0,
    "latitude": 0
  },
  "startTime": "string",
  "rentalTimePeriod": 0,
  "extendTimePeriod": 0,
  "originalPrice": 0,
  "discounts": [
    {
      "discountId": 0,
      "type": "string",
      "num": 0,
      "name": "string"
    }
  ],
  "rentalPrice": 0,
  "extendPrice": 0,
  "createTime": "string",
  "status": "string"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|[order](#schemaorder)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|none|Inline|

### 返回数据结构

状态码 **200**

*订单*

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» orderId|integer|true|none||订单id|
|» scooter|object|true|none||车|
|»» scooterId|integer|true|none||车id|
|»» type|string|true|none||型号|
|»» status|string|true|none||none|
|»» stationId|integer|true|none||所属站点的id|
|» station|[station](#schemastation)|true|none||none|
|»» stationId|integer|true|none||站点id|
|»» name|string|true|none||none|
|»» longitude|number|true|none||经度|
|»» latitude|number|true|none||纬度|
|» startTime|string|true|none||订单开始时间|
|» rentalTimePeriod|integer|true|none||订单时长（分钟，不包含延长）|
|» extendTimePeriod|integer|true|none||延长总时长|
|» originalPrice|number|true|none||订单原价|
|» discounts|[[discount](#schemadiscount)]|true|none||命中的折扣|
|»» discountId|integer|true|none||优惠id|
|»» type|string|true|none||优惠的类型|
|»» num|number|true|none||优惠的数额|
|»» name|string|true|none||命中优惠的名字|
|» rentalPrice|number|true|none||订单价格（包含折扣，不包含延长）|
|» extendPrice|number|true|none||延长价格（总价=订单价格+延长价格）|
|» createTime|string|true|none||订单下单时间|
|» status|string|true|none||订单状态|

#### 枚举值

|属性|值|
|---|---|
|type|X1 City Rider|
|type|E2 Pro Cruiser|
|type|S3 Speedster|
|type|L4 FlexMove|
|status|available|
|status|unavailable|
|status|maintenance|
|status|in_use|
|status|deleted|

状态码 **400**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||none|
|» message|string|true|none||none|

## PUT 修改信息

PUT /user/profile

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|userName|query|string| 否 |用户名|
|phoneNumber|query|string| 否 |联系电话|

> 返回示例

> 200 Response

```json
{
  "message": "string"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» message|string|true|none||none|

状态码 **400**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||none|
|» message|string|true|none||none|

## POST 添加信用卡

POST /user/card/add

一个用户绑定一张。如果已经绑定了再次绑定会直接替换。

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|cardNumber|query|string| 否 |信用卡账号|
|cardTokenHash|query|string| 否 |信用卡支付令牌|

> 返回示例

> 200 Response

```json
{
  "message": "string"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» message|string|true|none||none|

状态码 **400**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||none|
|» message|string|true|none||none|

## DELETE 删除信用卡

DELETE /user/card/delete

一个用户绑定一张。如果已经绑定了再次绑定会直接替换。

> 返回示例

> 200 Response

```json
{
  "message": "string"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» message|string|true|none||none|

状态码 **400**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||none|
|» message|string|true|none||none|

## GET 获取指定订单信息

GET /user/order/{orderId}

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|orderId|path|integer| 是 |none|

> 返回示例

> 200 Response

```json
{
  "orderId": 0,
  "scooter": {
    "scooterId": 0,
    "type": "X1 City Rider",
    "status": "available",
    "stationId": 0
  },
  "station": {
    "stationId": 0,
    "name": "string",
    "longitude": 0,
    "latitude": 0
  },
  "startTime": "string",
  "rentalTimePeriod": 0,
  "extendTimePeriod": 0,
  "originalPrice": 0,
  "discounts": [
    {
      "discountId": 0,
      "type": "string",
      "num": 0,
      "name": "string"
    }
  ],
  "rentalPrice": 0,
  "extendPrice": 0,
  "createTime": "string",
  "status": "string"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|[order](#schemaorder)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|none|Inline|

### 返回数据结构

状态码 **200**

*订单*

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» orderId|integer|true|none||订单id|
|» scooter|object|true|none||车|
|»» scooterId|integer|true|none||车id|
|»» type|string|true|none||型号|
|»» status|string|true|none||none|
|»» stationId|integer|true|none||所属站点的id|
|» station|[station](#schemastation)|true|none||none|
|»» stationId|integer|true|none||站点id|
|»» name|string|true|none||none|
|»» longitude|number|true|none||经度|
|»» latitude|number|true|none||纬度|
|» startTime|string|true|none||订单开始时间|
|» rentalTimePeriod|integer|true|none||订单时长（分钟，不包含延长）|
|» extendTimePeriod|integer|true|none||延长总时长|
|» originalPrice|number|true|none||订单原价|
|» discounts|[[discount](#schemadiscount)]|true|none||命中的折扣|
|»» discountId|integer|true|none||优惠id|
|»» type|string|true|none||优惠的类型|
|»» num|number|true|none||优惠的数额|
|»» name|string|true|none||命中优惠的名字|
|» rentalPrice|number|true|none||订单价格（包含折扣，不包含延长）|
|» extendPrice|number|true|none||延长价格（总价=订单价格+延长价格）|
|» createTime|string|true|none||订单下单时间|
|» status|string|true|none||订单状态|

#### 枚举值

|属性|值|
|---|---|
|type|X1 City Rider|
|type|E2 Pro Cruiser|
|type|S3 Speedster|
|type|L4 FlexMove|
|status|available|
|status|unavailable|
|status|maintenance|
|status|in_use|
|status|deleted|

状态码 **400**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||none|
|» message|string|true|none||none|

## GET 获取全部订单信息

GET /user/orders

> 返回示例

> 200 Response

```json
{
  "orders": [
    {
      "orderId": 0,
      "scooter": {
        "scooterId": 0,
        "type": "X1 City Rider",
        "status": "available",
        "stationId": 0
      },
      "station": {
        "stationId": 0,
        "name": "string",
        "longitude": 0,
        "latitude": 0
      },
      "startTime": "string",
      "rentalTimePeriod": 0,
      "extendTimePeriod": 0,
      "originalPrice": 0,
      "discounts": [
        {
          "discountId": 0,
          "type": "string",
          "num": 0,
          "name": "string"
        }
      ],
      "rentalPrice": 0,
      "extendPrice": 0,
      "createTime": "string",
      "status": "string"
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» orders|[[order](#schemaorder)]|true|none||[订单]|
|»» orderId|integer|true|none||订单id|
|»» scooter|object|true|none||车|
|»»» scooterId|integer|true|none||车id|
|»»» type|string|true|none||型号|
|»»» status|string|true|none||none|
|»»» stationId|integer|true|none||所属站点的id|
|»» station|[station](#schemastation)|true|none||none|
|»»» stationId|integer|true|none||站点id|
|»»» name|string|true|none||none|
|»»» longitude|number|true|none||经度|
|»»» latitude|number|true|none||纬度|
|»» startTime|string|true|none||订单开始时间|
|»» rentalTimePeriod|integer|true|none||订单时长（分钟，不包含延长）|
|»» extendTimePeriod|integer|true|none||延长总时长|
|»» originalPrice|number|true|none||订单原价|
|»» discounts|[[discount](#schemadiscount)]|true|none||命中的折扣|
|»»» discountId|integer|true|none||优惠id|
|»»» type|string|true|none||优惠的类型|
|»»» num|number|true|none||优惠的数额|
|»»» name|string|true|none||命中优惠的名字|
|»» rentalPrice|number|true|none||订单价格（包含折扣，不包含延长）|
|»» extendPrice|number|true|none||延长价格（总价=订单价格+延长价格）|
|»» createTime|string|true|none||订单下单时间|
|»» status|string|true|none||订单状态|

#### 枚举值

|属性|值|
|---|---|
|type|X1 City Rider|
|type|E2 Pro Cruiser|
|type|S3 Speedster|
|type|L4 FlexMove|
|status|available|
|status|unavailable|
|status|maintenance|
|status|in_use|
|status|deleted|

状态码 **400**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||none|
|» message|string|true|none||none|

## POST 支付订单

POST /user/order/{orderId}/pay

支付订单，后端调取数据库中信用卡信息直接支付，后端保存支付订单

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|orderId|path|integer| 是 |none|
|paymentMethod|query|string| 否 |none|

> 返回示例

> 200 Response

```json
{
  "message": "string"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» message|string|true|none||none|

状态码 **400**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||none|
|» message|string|true|none||none|

## PUT 延长时间

PUT /user/order/{orderId}/extend

调用之后修改订单延长时间，同时添加一条支付记录。

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|orderId|path|integer| 是 |none|
|extendTimePeriod|query|integer| 否 |延长的时间|
|paymentMethod|query|string| 否 |none|

> 返回示例

> 200 Response

```json
{
  "message": "string"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» message|string|true|none||说明成功还是失败|

## PUT 结束订单（还车）

PUT /user/order/{orderId}/return

后端结束订单

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|orderId|path|integer| 是 |none|

> 返回示例

> 200 Response

```json
{
  "message": "string"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» message|string|true|none||none|

## POST 提交用户反馈

POST /user/feedback/submit

发生故障时上报反馈

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|orderId|query|integer| 否 |订单id|
|region|query|string| 否 |故障类型|
|description|query|string| 否 |出现的具体故障的信息|

> 返回示例

> 200 Response

```json
{
  "message": "string"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» message|string|true|none||return自定义信息|

## POST 用户认证

POST /user/verify

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|groupName|query|string| 否 |none|

> 返回示例

> 200 Response

```json
{
  "message": "string",
  "expirationTime": "string"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» message|string|true|none||none|
|» expirationTime|string|true|none|认证过期时间|none|

状态码 **400**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||none|
|» message|string|true|none||none|

## DELETE 取消预定订单

DELETE /user/order/{orderId}/cancel

预定订单在预定的使用时间前可以取消，退还支付金额

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|orderId|path|integer| 是 |none|

> 返回示例

> 200 Response

```json
{
  "message": "string"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» message|string|true|none||none|

# 数据模型

<h2 id="tocS_discount">discount</h2>

<a id="schemadiscount"></a>
<a id="schema_discount"></a>
<a id="tocSdiscount"></a>
<a id="tocsdiscount"></a>

```json
{
  "discountId": 0,
  "type": "string",
  "num": 0,
  "name": "string"
}

```

命中的折扣

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|discountId|integer|true|none||优惠id|
|type|string|true|none||优惠的类型|
|num|number|true|none||优惠的数额|
|name|string|true|none||命中优惠的名字|

<h2 id="tocS_scooter">scooter</h2>

<a id="schemascooter"></a>
<a id="schema_scooter"></a>
<a id="tocSscooter"></a>
<a id="tocsscooter"></a>

```json
{
  "scooterId": 0,
  "longitude": 0,
  "latitude": 0,
  "type": "X1 City Rider",
  "battery": 0,
  "status": "available",
  "stationId": 0
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|scooterId|integer|true|none||车id|
|longitude|number|true|none||经度|
|latitude|number|true|none||纬度|
|type|string|true|none||型号|
|battery|number|true|none||电量（0.83）|
|status|string|true|none||none|
|stationId|integer|true|none||所属站点的id|

#### 枚举值

|属性|值|
|---|---|
|type|X1 City Rider|
|type|E2 Pro Cruiser|
|type|S3 Speedster|
|type|L4 FlexMove|
|status|available|
|status|unavailable|
|status|maintenance|
|status|in_use|
|status|deleted|

<h2 id="tocS_station">station</h2>

<a id="schemastation"></a>
<a id="schema_station"></a>
<a id="tocSstation"></a>
<a id="tocsstation"></a>

```json
{
  "stationId": 0,
  "name": "string",
  "longitude": 0,
  "latitude": 0
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|stationId|integer|true|none||站点id|
|name|string|true|none||none|
|longitude|number|true|none||经度|
|latitude|number|true|none||纬度|

<h2 id="tocS_order">order</h2>

<a id="schemaorder"></a>
<a id="schema_order"></a>
<a id="tocSorder"></a>
<a id="tocsorder"></a>

```json
{
  "orderId": 0,
  "scooter": {
    "scooterId": 0,
    "type": "X1 City Rider",
    "status": "available",
    "stationId": 0
  },
  "station": {
    "stationId": 0,
    "name": "string",
    "longitude": 0,
    "latitude": 0
  },
  "startTime": "string",
  "rentalTimePeriod": 0,
  "extendTimePeriod": 0,
  "originalPrice": 0,
  "discounts": [
    {
      "discountId": 0,
      "type": "string",
      "num": 0,
      "name": "string"
    }
  ],
  "rentalPrice": 0,
  "extendPrice": 0,
  "createTime": "string",
  "status": "string"
}

```

订单

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|orderId|integer|true|none||订单id|
|scooter|object|true|none||车|
|» scooterId|integer|true|none||车id|
|» type|string|true|none||型号|
|» status|string|true|none||none|
|» stationId|integer|true|none||所属站点的id|
|station|[station](#schemastation)|true|none||none|
|startTime|string|true|none||订单开始时间|
|rentalTimePeriod|integer|true|none||订单时长（分钟，不包含延长）|
|extendTimePeriod|integer|true|none||延长总时长|
|originalPrice|number|true|none||订单原价|
|discounts|[[discount](#schemadiscount)]|true|none||命中的折扣|
|rentalPrice|number|true|none||订单价格（包含折扣，不包含延长）|
|extendPrice|number|true|none||延长价格（总价=订单价格+延长价格）|
|createTime|string|true|none||订单下单时间|
|status|string|true|none||订单状态|

#### 枚举值

|属性|值|
|---|---|
|type|X1 City Rider|
|type|E2 Pro Cruiser|
|type|S3 Speedster|
|type|L4 FlexMove|
|status|available|
|status|unavailable|
|status|maintenance|
|status|in_use|
|status|deleted|

