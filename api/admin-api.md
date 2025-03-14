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

# 管理端

## GET 获取所有车和站点的信息

GET /bike_site_info

是否需要查询功能？分页？假设有分页

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|admin_id|query|string| 否 |管理员id|
|token|query|string| 否 |令牌|

> 返回示例

> 200 Response

```json
{
  "site_info": [
    {
      "stationId": 0,
      "name": "string",
      "longitude": 0,
      "latitude": 0,
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
|» site_info|[object]|true|none||none|
|»» stationId|integer|true|none||站点id|
|»» name|string|true|none||none|
|»» longitude|number|true|none||经度|
|»» latitude|number|true|none||纬度|
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
|type|X1 City Rider|
|type|E2 Pro Cruiser|
|type|S3 Speedster|
|type|L4 FlexMove|
|status|available|
|status|unavailable|
|status|maintenance|
|status|in_use|
|status|deleted|

## GET 显示统计数据

GET /calculate

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|admin_id|query|string| 否 |none|
|token|query|string| 否 |none|

> 返回示例

> 200 Response

```json
{
  "weekly_data": {
    "daily_income": [
      0
    ],
    "category_income": [
      {
        "length": "string",
        "income": "string"
      }
    ]
  },
  "weekly_discount_data": {
    "student_discount": [
      0
    ],
    "senior_discount": [
      0
    ],
    "frequent_discount": [
      0
    ]
  }
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
|» weekly_data|object|false|none|周内每日数据|none|
|»» daily_income|[number]|true|none||none|
|»» category_income|[object]|true|none||分组|
|»»» length|string|true|none||none|
|»»» income|string|true|none||none|
|» weekly_discount_data|object|true|none||none|
|»» student_discount|[number]|true|none||none|
|»» senior_discount|[number]|true|none||none|
|»» frequent_discount|[number]|true|none||none|

## GET 获取所有用户信息

GET /user_info

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|admin_id|query|string| 否 |管理员id|
|token|query|string| 否 |用户令牌|
|current_page_number|query|integer| 否 |none|
|item_per_page|query|integer| 否 |none|

> 返回示例

> 200 Response

```json
{
  "user_info": [
    {
      "id": 0,
      "name": "string",
      "email": "string",
      "phone_number": "string",
      "is_banned": true,
      "group": "common"
    }
  ],
  "page": {
    "currentPageNumber": 0,
    "totalPageNumber": 0,
    "itemPerPage": 0
  }
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
|» user_info|[object]|true|none||none|
|»» id|integer|true|none||用户的id|
|»» name|string|true|none||用户名|
|»» email|string|true|none||用户邮箱|
|»» phone_number|string|true|none||联系电话|
|»» is_banned|boolean|true|none||用户状态（是否被封禁）|
|»» group|string|true|none||用户所在的用户组|
|» page|object|true|none||none|
|»» currentPageNumber|integer|true|none||none|
|»» totalPageNumber|integer|true|none||none|
|»» itemPerPage|integer|true|none||none|

#### 枚举值

|属性|值|
|---|---|
|group|common|
|group|student|
|group|senior|

## POST 管理员登录

POST /login

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|username|query|string| 否 |管理员名|
|password|query|string| 否 |管理员密码（hash加密）|

> 返回示例

> 200 Response

```json
{
  "token": "string",
  "admin_id": "string"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

*用户令牌*

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» token|string|true|none|用户令牌|none|
|» admin_id|string|true|none|管理员id|ID 编号|

## POST 封禁用户

POST /change/ban

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|admin_id|query|string| 否 |none|
|token|query|string| 否 |none|
|user_id|query|integer| 否 |none|
|if_ban|query|boolean| 否 |none|

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

## DELETE 删除用户信息

DELETE /delete/user

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|admin_id|query|string| 否 |none|
|token|query|string| 否 |none|
|user_id|query|integer| 否 |none|

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

## POST 修改车信息

POST /change/bike

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|admin_id|query|string| 否 |none|
|token|query|string| 否 |none|
|scooter_id|query|integer| 否 |none|
|scooter_type|query|string| 否 |none|
|battery|query|string| 否 |none|
|longitude|query|string| 否 |none|
|latitude|query|string| 否 |none|
|status|query|string| 否 |状态|
|site_id|query|integer| 否 |none|

#### 枚举值

|属性|值|
|---|---|
|scooter_type|X1 City Rider|
|scooter_type|E2 Pro Cruiser|
|scooter_type|S3 Speedster|
|scooter_type|L4 FlexMove|
|status|availabe|
|status|disabled|
|status|maintance|
|status|in_use|

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

## POST 修改站点信息

POST /change/site

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|admin_id|query|string| 否 |none|
|token|query|string| 否 |none|
|site_id|query|integer| 否 |站点id|
|site_name|query|string| 否 |none|
|longitude|query|number| 否 |经度|
|latitude|query|number| 否 |纬度|

#### 详细说明

**latitude**: 纬度

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

## GET 获取反馈信息

GET /get/feedback

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|admin_id|query|string| 否 |用户id|
|token|query|string| 否 |令牌|
|current_page_number|query|integer| 否 |none|
|item_per_page|query|integer| 否 |none|

> 返回示例

> 200 Response

```json
{
  "feedback": [
    {
      "id": 0,
      "state": "unhandled",
      "rental_id": 0,
      "type": "string",
      "priority": 0,
      "created_time": "string",
      "update_time": "string"
    }
  ],
  "page": {
    "currentPageNumber": 0,
    "totalPageNumber": 0,
    "itemPerPage": 0
  }
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
|» feedback|[object]|true|none||none|
|»» id|integer|true|none||反馈id|
|»» state|string|true|none||反馈处理状态|
|»» rental_id|integer|true|none||反馈关联的订单|
|»» type|string|true|none||反馈类型id|
|»» priority|integer|true|none||优先级id|
|»» created_time|string|true|none||创建时间|
|»» update_time|string|true|none||更新时间|
|» page|object|true|none||none|
|»» currentPageNumber|integer|true|none||none|
|»» totalPageNumber|integer|true|none||none|
|»» itemPerPage|integer|true|none||none|

#### 枚举值

|属性|值|
|---|---|
|state|unhandled|
|state|handeled|

## POST 编辑车类型单价

POST /change/mode

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|admin_id|query|string| 否 |none|
|token|query|string| 否 |令牌|
|type|query|string| 否 |车类型名称|
|price|query|string| 否 |修改单价|

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

## POST 处理反馈信息

POST /post/feedback

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|admin_id|query|string| 否 |用户id|
|token|query|string| 否 |令牌|
|feedback_id|query|integer| 否 |反馈id|
|response|query|string| 否 |反馈处理结果|

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

## POST 添加车信息

POST /add/bike

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|admin_id|query|string| 否 |none|
|token|query|string| 否 |none|
|type|query|string| 是 |none|
|site_id|query|integer| 否 |none|
|battery|query|string| 是 |none|
|status|query|string| 是 |状态|

#### 枚举值

|属性|值|
|---|---|
|type|X1 City Rider|
|type|E2 Pro Cruiser|
|type|S3 Speedster|
|type|L4 FlexMove|
|status|usable|
|status|disabled|
|status|maintance|

> 返回示例

> 200 Response

```json
{}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

## DELETE 删除车信息

DELETE /delete/bike

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|admin_id|query|string| 否 |none|
|token|query|string| 否 |none|
|scooter_id|query|string| 否 |none|

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

## POST 未登录用户租车请求

POST /unregister_rent

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|admin_id|query|string| 否 |none|
|token|query|string| 否 |none|
|email|query|string| 否 |none|
|scooter_id|query|integer| 否 |none|
|start_time|query|string| 否 |none|
|time_period|query|integer| 否 |none|

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

## POST 结束未登录用户订单

POST /finish_order

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|admin_id|query|string| 否 |none|
|token|query|string| 否 |none|
|rental_id|query|integer| 否 |none|

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

## GET 查看所有订单

GET /get/all_rental

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|admin_id|query|string| 否 |none|
|token|query|string| 否 |none|
|user_registered|query|boolean| 否 |筛选条件：用户是否 登录|
|rental_status|query|string| 否 |筛选条件：订单状态|
|current_page_number|query|integer| 否 |none|
|item_peer_page|query|integer| 否 |none|

#### 枚举值

|属性|值|
|---|---|
|rental_status|not_started|
|rental_status|in_use|
|rental_status|unpaid|
|rental_status|finished|

> 返回示例

> 200 Response

```json
{
  "rental": [
    {
      "rental_id": 0,
      "user_id": 0,
      "email": "string",
      "scooter_id": 0,
      "start_time": "string",
      "rental_time_period": 0,
      "extend_time_period": 0,
      "discount_strategies": "string",
      "rental_price": 0,
      "extend_price": 0,
      "status": "not_started"
    }
  ],
  "page": {
    "currentPageNumber": 0,
    "totalPageNumber": 0,
    "itemPerPage": 0
  }
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
|» rental|[object]|true|none||none|
|»» rental_id|integer|true|none||none|
|»» user_id|integer|false|none||none|
|»» email|string|false|none||none|
|»» scooter_id|integer|true|none||none|
|»» start_time|string|true|none||none|
|»» rental_time_period|integer|true|none||分钟|
|»» extend_time_period|integer|false|none||分钟|
|»» discount_strategies|string|false|none||none|
|»» rental_price|number|true|none||none|
|»» extend_price|number|false|none||none|
|»» status|string|true|none||none|
|» page|object|true|none||none|
|»» currentPageNumber|integer|true|none||none|
|»» totalPageNumber|integer|true|none||none|
|»» itemPerPage|integer|true|none||none|

#### 枚举值

|属性|值|
|---|---|
|status|not_started|
|status|in_use|
|status|unpaid|
|status|finished|

## GET 获取所有车类型信息

GET /gettype

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|admin_id|query|string| 是 |none|
|token|query|string| 否 |none|

> 返回示例

> 200 Response

```json
{
  "scooters": [
    {
      "id": "string",
      "description": "string",
      "name": "string",
      "basePrice": 0,
      "minutePrice": 0,
      "maxDailyPrice": 0
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
|» scooters|[[type](#schematype)]|true|none||ID 编号|
|»» id|string|true|none||ID 编号|
|»» description|string|true|none||none|
|»» name|string|true|none||none|
|»» basePrice|number|true|none||none|
|»» minutePrice|number|true|none||none|
|»» maxDailyPrice|number|true|none||none|

# 数据模型

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

<h2 id="tocS_page">page</h2>

<a id="schemapage"></a>
<a id="schema_page"></a>
<a id="tocSpage"></a>
<a id="tocspage"></a>

```json
{
  "currentPageNumber": 0,
  "totalPageNumber": 0,
  "itemPerPage": 0
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|currentPageNumber|integer|true|none||none|
|totalPageNumber|integer|true|none||none|
|itemPerPage|integer|true|none||none|

<h2 id="tocS_type">type</h2>

<a id="schematype"></a>
<a id="schema_type"></a>
<a id="tocStype"></a>
<a id="tocstype"></a>

```json
{
  "id": "string",
  "description": "string",
  "name": "string",
  "basePrice": 0,
  "minutePrice": 0,
  "maxDailyPrice": 0
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|string|true|none||ID 编号|
|description|string|true|none||none|
|name|string|true|none||none|
|basePrice|number|true|none||none|
|minutePrice|number|true|none||none|
|maxDailyPrice|number|true|none||none|

