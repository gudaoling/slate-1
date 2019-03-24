---

title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>

includes:
  - sign
  - errors

search: true
---

# Introduction

Welcome to Kinot open platform!You can use our API to access Lora device API endpoints, which can get information on various parking lock,parking sensor in our database.

# Authentication

Each interface must be authorized, so calling <a href='#sign'>each interface </a> requires the use of public request
parameters. For details, please refer to[[请求签名说明文档](https://help.aliyun.com/document_detail/29475.html?spm=a2c4g.11186623.6.572.f7ee2ca7sdQgGP)].[English](https://www.alibabacloud.com/help/doc-detail/29475.htm?spm=a2c63.p38356.b99.31.58d86accQr5HRF)



Precautions:

Please turn to administrator for AppKey and AppSecret used
for signature. To facilitate developer debugging, the SDK for Postman and other
development languages are provided for your reference.

[Request signing and debugging of API
gateway through Postman](https://help.aliyun.com/document_detail/93641.html?spm=a2c4g.11186623.6.573.438332d8A3Zxon)

#### SDK Reference

| Language | URL                                                    |
| -------- | ------------------------------------------------------ |
| Node.js  | https://github.com/aliyun/api-gateway-nodejs-sdk       |
| .Net     | https://github.com/aliyun/api-gateway-demo-sign-net    |
| Python   | https://github.com/aliyun/api-gateway-demo-sign-python |
| PHP      | https://github.com/aliyun/api-gateway-demo-sign-php    |
|          |                                                        |

[FAQ](https://www.alibabacloud.com/help/doc-detail/43906.htm?spm=a2c63.p38356.b99.199.758075c2F8qMF6)




# <a name='api'>Parking lock(Lora)</a>

##  Get All Parking lock

```shell
curl -X GET "http://device.api.parks8.com/open/lora/v1/lockers?offset=0&limit=10"
     -H "Content-Type: application/json"
```



> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"OK",
    "objects":[
        {
            "sn":419631107,
            "voltage":3.659,
            "frequency":37.919,
            "locked":0,
            "car_detected":0,
            "shell_opened":0,
            "low_battery":0,
            "coil_fault":0,
            "bar_position_error":0,
            "motor_fail":0,
            "rs_si":0,
            "bt_match_code":"61518-59257-29505-55487-10411-15740",
            "bt_mac":"aa0018382001",
            "updated_at":"2019-03-13T10:42:39+08:00"
        }
    ],
    "count":1
}

```

This endpoint retrieves all parking locks.

### HTTP Request

`GET  http://device.api.parks8.com/open/open/lora/v1/lockers?offset=0&limit=10`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
offset | int | 0<=offset<=(count/limit)+1 
limit | int | 10<=limit<=100 

### <a name='locker'>Response body detail</a>

| Parameter          | Type   | Description                                        |
| ------------------ | ------ | -------------------------------------------------- |
| sn                 | int    | Parking lock SN                                    |
| voltage            | float  | Battery voltage in Milliamps (mv)                  |
| frequency          | float  | Loop coil frequency                                |
| locked             | int    | Lock status(0:down,1:up)                           |
| car_detected       | int    | Space detection(0：available,1:occupied)           |
| shell_opened       | int    | Cabinet open(0:Normal,1:open)                      |
| low_battery        | int    | Battery status(0:Normal,1:low power)               |
| coil_fault         | int    | Loop malfunction(0:normal,1:abnormal)              |
| bar_position_error | int    | Bar position malfunction(0:Normal,1:abnormal)      |
| motor_fail         | int    | Motor malfunction(0:Normal,1:abnormal)             |
| rs_si              | float  | Signal strength, around 0 indicate stronger signal |
| bt_match_code      | string | BlueTooth match code                               |
| bt_mac             | string | BlueTooth MAC                                      |
| updated_at         | string | Last update time                                   |



## Get a Specific Parking lock

```shell
curl -X GET "http://device.api.parks8.com/open/lora/v1/lockers/<sn>"
     -H "Content-Type: application/json"
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"OK",
    "objects":[
        {
            "sn":419631107,
            "voltage":3.659,
            "frequency":37.919,
            "locked":1,
            "car_detected":1,
            "shell_opened":0,
            "low_battery":0,
            "coil_fault":0,
            "bar_position_error":0,
            "motor_fail":0,
            "rs_si":0,
            "bt_match_code":"61518-59257-29505-55487-10411-15740",
            "bt_mac":"aa0018382001",
            "updated_at":"2019-03-13T10:42:39+08:00"
        }
    ],
}
```

This endpoint retrieves a specific parking lock.

### HTTP Request

`GET http://device.api.parks8.com/open/lora/v1/lockers/<sn>`

### URL Parameters

Parameter |Type | Description
--------- | -----------| -----------
sn |int | The SN of the parking lock to retrieve 

### Response body detail

| Parameter          | Type   | Description                     |
| ------------------ | ------ | ------------------------------- |
| sn                 | int    | <a href='#locker'>reference</a> |
| voltage            | float  |                                 |
| frequency          | float  |                                 |
| locked             | int    |                                 |
| car_detected       | int    |                                 |
| shell_opened       | int    |                                 |
| low_battery        | int    |                                 |
| coil_fault         | int    |                                 |
| bar_position_error | int    |                                 |
| motor_fail         | int    |                                 |
| rs_si              | float  |                                 |
| bt_match_code      | string |                                 |
| bt_mac             | string |                                 |
| updated_at         | string |                                 |





# Parking sensor(Lora)

## Get All Parking sensor

```shell
curl -X GET "http://device.api.parks8.com/open/lora/v1/sensors?offset=0&limit=10"
     -H "Content-Type: application/json"
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"OK",
    "objects":[
        {
            "sn":419635201,
            "voltage":3.654,
            "frequency":38.6,
            "active":1,
            "car_detected":1,
            "low_battery":1,
            "coil_fault":1,
            "rs_si":-109.5,
            "updated_at":"2019-03-13T10:42:39+08:00"
        }
    ],
   "count":1
}
```

This endpoint retrieves all parking sensor.

### HTTP Request

`GET http://device.api.parks8.com/open/lora/v1/sensors?offset=1&limit=10`

### Query Parameters

| Parameter | Type | Description                |
| --------- | ---- | -------------------------- |
| offset    | int  | 0<=offset<=(count/limit)+1 |
| limit     | int  | 10<=limit<=100             |

### <a name='sensor'>Response body detail</a>

| Parameter    | Type   | Description                                        |
| ------------ | ------ | -------------------------------------------------- |
| sn           | int    | Parking sensor SN                                  |
| voltage      | float  | Battery voltage in Milliamps (mv)                  |
| frequency    | float  | Loop coil frequency                                |
| car_detected | int    | Space detection(0：available,1:occupied)           |
| low_battery  | int    | Battery status(0:Normal,1:low power)               |
| coil_fault   | int    | Loop malfunction(0:normal,1:abnormal)              |
| rs_si        | float  | Signal strength, around 0 indicate stronger signal |
| updated_at   | string | Last update time                                   |



## Get a Specific Parking sensor

```shell
curl -X GET "http://device.api.parks8.com/open/lora/v1/sensors/<sn>"
     -H "Content-Type: application/json"
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"OK",
    "objects":[
        {
            "sn":419635201,
            "voltage":3.654,
            "frequency":38.6,
            "car_detected":1,
            "low_battery":1,
            "coil_fault":1,
            "rs_si":-109.5
        }
    ]
}
```

This endpoint retrieves a specific parking sensor.

### HTTP Request

`GET http://device.api.parks8.com/open/lora/v1/sensors/<sn>`

### URL Parameters

| Parameter | Type | Description                              |
| --------- | ---- | ---------------------------------------- |
| sn        | int  | The sn of the parking sensor to retrieve |

### Response body detail

| Parameter    | Type   | Description                     |
| ------------ | ------ | ------------------------------- |
| sn           | int    | <a href='#sensor'>reference</a> |
| voltage      | float  |                                 |
| frequency    | float  |                                 |
| car_detected | int    |                                 |
| low_battery  | int    |                                 |
| coil_fault   | int    |                                 |
| rs_si        | float  |                                 |
| updated_at   | string |                                 |





# Gateway Dtu Device (Lora)

## Get a Specific Dtu device

```shell
curl -X GET "http://device.api.parks8.com/open/lora/v1/dtu_devices/<sn>"
     -H "Content-Type: application/json"
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"OK",
    "objects":[
        {
            "sn":644219880,
            "hw":4097,
            "sw":8193,
            "firmware":17,
            "host":"218.204.252.18:44062",
            "online":"online",
            "updated_at":"2019-03-24T17:03:44+08:00"
        }
    ]
}
```

This endpoint retrieves a specific Dtu device .

### HTTP Request

`GET http://device.api.parks8.com/open/lora/v1/dtu_devices/<sn>`

### URL Parameters

| Parameter | Type | Description                          |
| --------- | ---- | ------------------------------------ |
| sn        | int  | The SN of the Dtu device to retrieve |

### Response body detail

| Parameter  | Type   | Description           |
| ---------- | ------ | --------------------- |
| sn         | int    | Dtu SN                |
| hw         | int    | hardware version      |
| sw         | int    | software version      |
| firmware   | int    | firmware version      |
| host       | string | client host           |
| online     | string | ‘online’ or ‘offline’ |
| updated_at | string | last update time      |



# Command

##  Send command

```shell
curl -X POST "http://device.api.parks8.com/open/lora/v1/commands"
     -H "Content-Type: application/json"
```

> The above command request JSON structured like this:

```json
{
	"sn": 419635201,
	"command": 1,
	"parameter": {
		"key": "handle",
		"value": 1
	}
}
```

> The above command returns JSON structured like this:

```json
{
	"code": 0,
	"message": "OK",
	"objects": [{
		"sn": 419635201,
	    "guid":"ED33B369589222DB25B298C6E06C5DAE",
		"command": 1,
	  	"command_status": "pending",
		"parameter": {
			"key": "handle",
			"value": 1
		}
	}]
}
```



### HTTP Request

`POST http://device.api.parks8.com/open/lora/v1/commands`

### Request body detail

| Parameter | Type | Description                                                  |
| --------- | ---- | ------------------------------------------------------------ |
| sn        | int  | It can be a Parking sensor SN or a Parking lock Sn           |
| command   | int  | Fixed value of 1                                             |
| parameter | JSON | 1.If SN is parking lock, value=1 represents reset BlueTooth match code                        2.If SN is parking sensor,value=1 represents activation of equipment,value=2 represents  freezing of equipment. |

### Response body detail

| Parameter      | Type   | Description                                                 |
| -------------- | ------ | ----------------------------------------------------------- |
| guid           | string | guid                                                        |
| sn             | int    |                                                             |
| command        | int    |                                                             |
| commnad_status | string | command state(sending=>pending=>arrived=>succeeded=>failed) |
| parameter      | json   |                                                             |



##  Get a Specific Command 

```shell
curl -X GET "http://device.api.parks8.com/open/lora/v1/commands?guid=<guid>"
     -H "Content-Type: application/json"
```

> The above command returns JSON structured like this:

```json
{
	"code": 0,
	"message": "OK",
	"objects": [{
		"sn": 419635201,
	    "guid":"ED33B369589222DB25B298C6E06C5DAE",
		"command": 1,
	  	"command_status": "pending",
		"parameter": {
			"key": "default",
			"value": 1
		}
	}]
}
```



### HTTP Request

`GET http://device.api.parks8.com/open/lora/v1/commands?guid=<guid>`

### Query Parameters

| Parameter | Type   | Description                        |
| --------- | ------ | ---------------------------------- |
| guid      | string | returned after sending the command |

### Response body detail

| Parameter      | Type   | Description                                                 |
| -------------- | ------ | ----------------------------------------------------------- |
| guid           | string |                                                             |
| sn             | int    |                                                             |
| command        | int    |                                                             |
| commnad_status | string | command state(sending=>pending=>arrived=>succeeded=>failed) |
| parameter      | json   |                                                             |





#  Subscribe

##  Set  notification configuration info

```shell

curl -X POST "http://device.api.parks8.com/open/lora/v1/notifications"
     -H "Content-Type: application/json"
```

> The above command request JSON structured like this:

```json
{
    "device_type": 34, 
    "status_changed_callback_url": "<your_callback_url>", 
    "command_resp_callback_url": "<your_callback_url>"
}
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"OK",
    "objects":[
        {
            "device_type":34,
            "status_changed_callback_url":3.654,
            "command_resp_callback_url":38.6
        }
    ]
}
```



### HTTP Request

`POST http://device.api.parks8.com/open/lora/v1/notifications`

### Request body detail

| Parameter                   | Type   | Description                                                 |
| --------------------------- | ------ | ----------------------------------------------------------- |
| device_type                 | int    | number 18 means parking lock,number 34 means parking sensor |
| status_changed_callback_url | string |                                                             |
| commandResp_callback_url    | string |                                                             |

## Get notification configuration info

```shell
curl -X GET "http://device.api.parks8.com/open/lora/v1/notifications?device_type=<18>"
     -H "Content-Type: application/json"
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"OK",
    "objects":[
        {
            "device_type":18,
            "status_changed_callback_url":3.654,
            "command_resp_callback_url":38.6,
            "update_at":"2019-03-13T10:42:39+08:00",
        }
    ]
}
```



### HTTP Request

`GET http://device.api.parks8.com/open/lora/v1/notifications?device_type=<18>`

### Query Parameters

| Parameter   | Type | Description                                                 |
| ----------- | ---- | ----------------------------------------------------------- |
| device_type | int  | number 18 means parking lock,number 34 means parking sensor |



##  Test notification

```shell
curl -X POST "http://device.api.parks8.com/open/lora/v1/test/notifications"
     -H ""Content-Type: application/json"
```

> The above command request JSON structured like this:

```json
{
    "sn": 419631107, 
    "callback_type": "status_changed"
}
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"OK",
    "request_id":"19feab9dace17f0f9c6136969c621d76",
    "objects":[
        {
            "sn":419631107,
            "callback_url":"http://192.168.16.238/test",
            "error_detail":"sent"
        }
    ]
}
```

This interface is used to test whether the callback address of each setting receives data normally.

### HTTP Request

`POST http://device.api.parks8.com/open/lora/v1/test/notifications`

### Request body detail

| Parameter     | Type   | Description                                |
| ------------- | ------ | ------------------------------------------ |
| sn            | int    |                                            |
| callback_type | string | 2 option (“status_changed”,“command_resp”) |





# Notify-parking lock(Lora)

##  Status changed

```shell
curl -X POST "<your_callback_url>"
     -H "Content-Type: application/json"
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
    "sign":"641EB269A46944D404EC6BEF902E7918",
    "device_type":38,
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

| Parameter          | Type   | Description                                |
| ------------------ | ------ | ------------------------------------------ |
| sn                 | int    | <a href='#locker'>reference</a>            |
| voltage            | float  |                                            |
| frequency          | float  |                                            |
| locked             | int    |                                            |
| car_detected       | int    |                                            |
| shell_opened       | int    |                                            |
| low_battery        | int    |                                            |
| coil_fault         | int    |                                            |
| bar_position_error | int    |                                            |
| motor_fail         | int    |                                            |
| rs_si              | float  |                                            |
| updated_at         | string |                                            |
| sign               | string | signature string  ,<a href='#sign'>See</a> |
| device_type        | int    |                                            |

## Command changed

```shell
curl -X POST "<your_callback_url>"
     -H "Content-Type: application/json"
```

> The above command request JSON structured like this:

```json
{
    "guid": "3019FF21F07FA9EFD7CA1DBBE8AF3749",
	"sn": 419631107,
	"commnad_status": "succeeded",
	"reason":"NULL",
    "updated_at": "2019-03-13T10:42:39+08:00",
    "sign":"641EB269A46944D404EC6BEF902E7918",
     "device_type":38,
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

| Parameter      | Type   | Description                                                 |
| -------------- | ------ | ----------------------------------------------------------- |
| guid           | string | guid                                                        |
| sn             | int    | SN of parking lock                                          |
| commnad_status | string | command state(sending=>pending=>arrived=>succeeded=>failed) |
| reason         | string | reason of failed                                            |
| updated_at     | string | last update time                                            |
| sign           | string | signature string ,<a href='#sign'>See</a>                   |
| device_type    | int    |                                                             |

# Notify-parking sensor(Lora)

##  Status changed

```shell
curl -X POST "<your_callback_url>"
     -H "Content-Type: application/json"
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
    "sign":"641EB269A46944D404EC6BEF902E7918",
    "device_type":38,
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

| Parameter    | Type   | Description                              |
| ------------ | ------ | ---------------------------------------- |
| sn           | int    | <a href='#sensor'>reference</a>          |
| voltage      | float  |                                          |
| frequency    | float  |                                          |
| car_detected | int    |                                          |
| low_battery  | int    |                                          |
| coil_fault   | int    |                                          |
| rs_si        | float  |                                          |
| updated_at   | string |                                          |
| sign         | string | signature string,<a href='#sign'>See</a> |
| device_type  | int    |                                          |

## Command changed

```shell
curl -X POST "<your_callback_url>"
     -H "Content-Type: application/json"
```

> The above command request JSON structured like this:

```json
{
    "guid": "3019FF21F07FA9EFD7CA1DBBE8AF3749",
	"sn": 419631107,
	"commnad_status": "succeeded",
	"reason":"NULL",
    "updated_at": "2019-03-13T10:42:39+08:00",
    "sign":"641EB269A46944D404EC6BEF902E7918",
    "device_type":34,
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

| Parameter      | Type   | Description                                                 |
| -------------- | ------ | ----------------------------------------------------------- |
| guid           | string | guid                                                        |
| sn             | int    | SN of parking sensor                                        |
| commnad_status | string | command state(sending=>pending=>arrived=>succeeded=>failed) |
| reason         | string | reason of failed                                            |
| updated_at     | string | last update time                                            |
| sign           | string | signature string ,<a href='#sign'>See</a>                   |
| device_type    | int    |                                                             |
