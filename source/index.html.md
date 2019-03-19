---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

欢迎使用Lora设备数据平台! 你可以使用我们提供的API去获取数据库中的各种车位小锁、车位雷达等信息

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
```

### 公共入参

公共请求参数是指每个接口都需要使用到的请求参数。

| 参数名称               | 位置   | 必须 | 描述                                                         |
| ---------------------- | ------ | ---- | ------------------------------------------------------------ |
| X-Ca-Key               | Header | 是   | Appkey，调用API的身份标识，可以到阿里云[API网关控制台](https://apigateway.console.aliyun.com/#/apps/list)申请 |
| X-Ca-Signature         | Header | 是   | 通过签名计算规则计算的请求签名串，参照：[签名计算规则](#Signature) |
| X-Ca-Timestamp         | Header | 否   | API 调用者传递时间戳，值为当前时间的毫秒数，也就是从1970年1月1日起至今的时间转换为毫秒，时间戳有效时间为15分钟 |
| X-Ca-Nonce             | Header | 否   | API请求的唯一标识符，15分钟内同一X-Ca-Nonce不能重复使用，建议使用 UUID，结合时间戳防重放 |
| Content-MD5            | Header | 否   | 当请求 Body 非 Form 表单时，需要计算 Body 的 MD5 值传递给云网关进行 Body MD5 校验 |
| X-Ca-Signature-Headers | Header | 否   | 指定哪些Header参与签名，支持多值以","分割，默认只有X-Ca-Key参与签名，为安全需要也请将X-Ca-Timestamp、X-Ca-Nonce进行签名，例如：X-X-Ca-Signature-Headers:Ca-Timestamp,X-Ca-Nonce |

### 签名计算规则

请求签名，是基于请求内容计算的数字签名，用于API识别用户身份。客户端调用API时，需要在请求中添加计算的签名（X-Ca-Signature）。

#### 签名计算流程

准备APPkey → 构造待签名字符串stringToSign → 使用Secret计算签名

##### 1.准备APPKey

Appkey，调用API的身份标识，可以到阿里云[API网关控制台](https://apigateway.console.aliyun.com/#/apps/list)申请

##### 2.构造待签名字符串stringToSign

```
String stringToSign=
HTTPMethod+"\n"+
Accept+"\n"+   //建议显示设置 Accept Header。当 Accept 为空时，部分 Http 客户端会给 Accept 设置默认值为 */*，导致签名校验失败。
Content-MD5+"\n"
Content-Type+"\n" +
Date+"\n"+
Headers +
Url
```

###### HTTPMethod

为全大写，如 POST。

```
Accept、Content-MD5、Content-Type、Date 如果为空也需要添加换行符”\n”，Headers如果为空不需要添加”\n”。
```

###### Content-MD5

Content-MD5 是指 Body 的 MD5 值，只有当 Body 非 Form 表单时才计算 MD5，计算方式为：

String content-MD5 = Base64.encodeBase64(MD5(bodyStream.getbytes("UTF-8"))); bodyStream 为字节数组。

###### Headers

Headers 是指参与 Headers 签名计算的 Header 的 Key、Value 拼接的字符串，建议对 X-Ca 开头以及自定义 Header 计算签名，注意如下参数不参与 Headers 签名计算：X-Ca-Signature、X-Ca-Signature-Headers、Accept、Content-MD5、Content-Type、Date。

###### Headers 组织方法：

先对参与 Headers 签名计算的 Header的Key 按照字典排序后使用如下方式拼接，如果某个 Header 的 Value 为空，则使用 HeaderKey + “:” + “\n”参与签名，需要保留 Key 和英文冒号。

```
String headers =
HeaderKey1 + ":" + HeaderValue1 + "\n"\+
HeaderKey2 + ":" + HeaderValue2 + "\n"\+
...
HeaderKeyN + ":" + HeaderValueN + "\n"
```

将 Headers 签名中 Header 的 Key 使用英文逗号分割放到 Request 的 Header 中，Key为：X-Ca-Signature-Headers。

###### Url

Url 指 Path + Query + Body 中 Form 参数，组织方法：对 Query+Form 参数按照字典对 Key 进行排序后按照如下方法拼接，如果 Query 或 Form 参数为空，则 Url = Path，不需要添加 ？，如果某个参数的 Value 为空只保留 Key 参与签名，等号不需要再加入签名。

```
String url =
Path +
"?" +
Key1 + "=" + Value1 +
"&" + Key2 + "=" + Value2 +
...
"&" + KeyN + "=" + ValueN
```

注意这里 Query 或 Form 参数的 Value 可能有多个，多个的时候只取第一个 Value 参与签名计算。

##### 3.使用Secret计算签名

```
Mac hmacSha256 = Mac.getInstance("HmacSHA256");
byte[] keyBytes = secret.getBytes("UTF-8");
hmacSha256.init(new SecretKeySpec(keyBytes, 0, keyBytes.length, "HmacSHA256"));
String sign = new String(Base64.encodeBase64(Sha256.doFinal(stringToSign.getBytes("UTF-8")),"UTF-8"));
```

Secret 为 APP 的密钥，请在[应用管理](https://apigateway.console.aliyun.com/#/apps/list)中获取。




# 1.Parking lockers

## 1.1 Get All Pakring lockers

```shell
curl -X GET "http://device.api.parks8.com/lora/v1/lockers"
```



> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"OK",
    "objects":[
        {
            "sn":419631107,
            "heartbeat":7036,
            "voltage":3.659,
            "frequency":37.919,
            "locked":7036,
            "car_detected":7036,
            "shell_opened":7036,
            "low_battery":7036,
            "coil_fault":7036,
            "bar_position_error":7036,
            "motor_fail":7036,
            "rs_si":0,
            "bt_match_code":"61518-59257-29505-55487-10411-15740",
            "bt_mac":"aa0018382001",
            "updated_at":"2019-03-13T10:42:39+08:00"
        }
    ],
    "count":1
}

```

This endpoint retrieves all parking lockers.

### HTTP Request

`GET  http://device.api.parks8.com/lora/v1/lockers`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## 1.2 Get a Specific Parking locker

```shell
curl -X GET "http://device.api.parks8.com/lora/v1/lockers/419631107"
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"OK",
    "objects":[
        {
            "sn":419631107,
            "heartbeat":7036,
            "voltage":3.659,
            "frequency":37.919,
            "locked":7036,
            "car_detected":7036,
            "shell_opened":7036,
            "low_battery":7036,
            "coil_fault":7036,
            "bar_position_error":7036,
            "motor_fail":7036,
            "rs_si":0,
            "bt_match_code":"61518-59257-29505-55487-10411-15740",
            "bt_mac":"aa0018382001",
            "updated_at":"2019-03-13T10:42:39+08:00"
        }
    ],
}
```

This endpoint retrieves a specific parking locker.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://device.api.parks8.com/lora/v1/lockers/<SN>`

### URL Parameters

Parameter | Description
--------- | -----------
SN | The SN of the parking locker to retrieve 



# 2.Parking sensors

## 2.1 Get All Parking sensors

```shell
curl -X GET "http://device.api.parks8.com/lora/v1/sensors"
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"OK",
    "objects":[
        {
            "sn":419635201,
            "heartbeat":36811,
            "voltage":3.654,
            "frequency":38.6,
            "active":1,
            "car_detected":1,
            "low_battery":1,
            "coil_fault":1,
            "rs_si":-109.5
        }
    ],
   "count":1
}
```

This endpoint retrieves all parking sensors.

### HTTP Request

`GET http://device.api.parks8.com/lora/v1/sensors`

### Query Parameters

| Parameter | Default | Description   |
| --------- | ------- | ------------- |
| pageNum   | 1       | 当前页码数.   |
| pageSize  | 20      | 每页显示数量. |

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## 2.2 Get a Specific Parking sensor

```shell
curl -X GET "http://device.api.parks8.com/lora/v1/sensors/419635201"
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"OK",
    "objects":[
        {
            "sn":419635201,
            "heartbeat":36811,
            "voltage":3.654,
            "frequency":38.6,
            "active":1,
            "car_detected":1,
            "low_battery":1,
            "coil_fault":1,
            "rs_si":-109.5
        }
    ]
}
```

This endpoint retrieves a specific parking sensor.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://device.api.parks8.com/lora/v1/sensors/<SN>`

### URL Parameters

| Parameter | Description                              |
| --------- | ---------------------------------------- |
| SN        | The SN of the parking sensor to retrieve |

# 3.订阅

## 3.1 设置设备信息变化回调地址

```shell
curl -X POST "http://device.api.parks8.com/lora/v1/subscribe"
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"OK",
    "objects":[
        {
            "sn":419635201,
            "heartbeat":36811,
            "voltage":3.654,
            "frequency":38.6,
            "active":1,
            "car_detected":1,
            "low_battery":1,
            "coil_fault":1,
            "rs_si":-109.5
        }
    ],
   "count":1
}
```

This endpoint retrieves all parking sensors.

### HTTP Request

`POST http://device.api.parks8.com/lora/v1/subscribe`

### Query Parameters

| Parameter | Default | Description   |
| --------- | ------- | ------------- |
| pageNum   | 1       | 当前页码数.   |
| pageSize  | 20      | 每页显示数量. |

## 3.2 获取设置设备信息变化回调地址

```shell
curl -X GET "http://device.api.parks8.com/lora/v1/subscribe"
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"OK",
    "objects":[
        {
            "device_type":38,
            "status_changed_callback_url":3.654,
            "commandResp_callback_url":38.6,
            "update_at":"2019-03-13T10:42:39+08:00",
        }
    ]
}
```

This endpoint retrieves a specific parking sensor.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://device.api.parks8.com/lora/v1/sensors/<SN>`

### URL Parameters

| Parameter | Description                              |
| --------- | ---------------------------------------- |
| SN        | The SN of the parking sensor to retrieve |

# 4.推送-车位小锁

## 4.1 状态变化

```shell
curl -X POST "<your_callback_url>"
```

> The above command request JSON structured like this:

```json
{
	"sn": 419631107,
	"voltage": 3.659,
	"frequency": 37.919,
	"locked": 0,
	"car_detected": 1,
	"shell_opened": 0,
	"low_battery": 0,
	"coil_fault": 0,
	"bar_position_error": 0,
	"motor_fail": 1,
	"rs_si": 1,
	"updated_at": "2019-03-13T10:42:39+08:00",
    "sign":"641EB269A46944D404EC6BEF902E7918"
}
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"OK"
}
```

### HTTP Request

`POST <your_callback_url>`

### Request body detail

| Parameter          | type   | Description |
| ------------------ | ------ | ----------- |
| sn                 | int    |             |
| voltage            | float  |             |
| frequency          | float  |             |
| locked             | int    |             |
| car_detected       | int    |             |
| shell_opened       | int    |             |
| low_battery        | int    |             |
| coil_fault         | int    |             |
| bar_position_error | int    |             |
| motor_fail         | int    |             |
| rs_si              | float  |             |
| updated_at         | string |             |
| sign               | string |             |
|                    |        |             |

## 4.2 命令变化

```shell
curl -X POST "<your_callback_url>"
```

> The above command request JSON structured like this:

```json
{
    "guid": "3019FF21F07FA9EFD7CA1DBBE8AF3749",
	"sn": 419631107,
	"commnad_status": "succeeded",
	"reason":"NULL",
    "updated_at": "2019-03-13T10:42:39+08:00",
    "sign":"641EB269A46944D404EC6BEF902E7918"
}
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"OK"
}
```

### HTTP Request

`POST <your_callback_url>`

### Request body detail

| Parameter      | type   | Description                                  |
| -------------- | ------ | -------------------------------------------- |
| guid           | string | guid                                         |
| sn             | int    | sn of parking locker                         |
| commnad_status | string | sending=>pending=>arrived=>succeeded=>failed |
| reason         | string | reason for failure                           |
| sign           | string |                                              |
|                |        |                                              |

# 5.推送-车位雷达

## 5.1 状态变化

```shell
curl -X POST "<your_callback_url>"
```

> The above command request JSON structured like this:

```json
{
	"sn": 419631107,
	"voltage": 3.659,
	"frequency": 37.919,
	"car_detected": 1,
	"low_battery": 0,
    "coil_fault": 0,
	"rs_si": 1,
	"updated_at": "2019-03-13T10:42:39+08:00",
    "sign":"641EB269A46944D404EC6BEF902E7918"
}
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"OK"
}
```

### HTTP Request

`POST <your_callback_url>`

### Request body detail

| Parameter    | type   | Description |
| ------------ | ------ | ----------- |
| sn           | int    |             |
| voltage      | float  |             |
| frequency    | float  |             |
| car_detected | int    |             |
| low_battery  | int    |             |
| coil_fault   | int    |             |
| rs_si        | float  |             |
| sign         | string |             |

## 5.2 命令变化

```shell
curl -X POST "<your_callback_url>"
```

> The above command request JSON structured like this:

```json
{
    "guid": "3019FF21F07FA9EFD7CA1DBBE8AF3749",
	"sn": 419631107,
	"commnad_status": "succeeded",
	"reason":"NULL",
    "updated_at": "2019-03-13T10:42:39+08:00",
    "sign":"641EB269A46944D404EC6BEF902E7918"
}
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"OK"
}
```

### HTTP Request

`POST <your_callback_url>`

### Request body detail

| Parameter      | type   | Description                                  |
| -------------- | ------ | -------------------------------------------- |
| guid           | string | guid                                         |
| sn             | int    | sn of parking sensor                         |
| commnad_status | string | sending=>pending=>arrived=>succeeded=>failed |
| reason         | string | reason for failure                           |
| updated_at     | string |                                              |
| sign           | string |                                              |
|                |        |                                              |

