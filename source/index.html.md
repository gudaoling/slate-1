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

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

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

