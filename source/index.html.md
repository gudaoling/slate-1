---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to Kinot open platform!You can use our API to access Lora device API endpoints, which can get information on various parking lockers,parking sensor in our database.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
```




# 1.Parking lockers(Lora)

## 1.1 Get All Parking lockers

```shell
curl -X GET "http://device.api.parks8.com/lora/v1/lockers?offset=1&limit=10"
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

This endpoint retrieves all parking lockers.

### HTTP Request

`GET  http://device.api.parks8.com/lora/v1/lockers?offset=1&limit=10`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
offset | int | 1<=offset<(count/limit) 
limit | int | 10<=limit<=100 

### Response body detail

| Parameter          | type   | Description                    |
| ------------------ | ------ | ------------------------------ |
| sn                 | int    | 车位小锁SN                     |
| voltage            | float  | 电池电压，计量单位为毫安(mv)   |
| frequency          | float  | 线圈频率                       |
| locked             | int    | 锁状态(0:下锁,1:上锁)          |
| car_detected       | int    | 车辆检测(0：无车,1:有车)       |
| shell_opened       | int    | 外壳打开(0:正常,1:打开)        |
| low_battery        | int    | 电池状态(0:正常,1:电量低)      |
| coil_fault         | int    | 线圈故障(0:正常,1:有故障)      |
| bar_position_error | int    | 栏位置故障(0:正常,1:有故障)    |
| motor_fail         | int    | 电机故障(0:正常,1:有故障)      |
| rs_si              | float  | 信号强度,趋于0上下表示信号较强 |
| bt_match_code      | string | 蓝牙匹配码                     |
| bt_mac             | string | 蓝牙MAC                        |
| updated_at         | string | 最后更新时间                   |



## 1.2 Get a Specific Parking locker

```shell
curl -X GET "http://device.api.parks8.com/lora/v1/lockers/<sn>"
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

### HTTP Request

`GET http://device.api.parks8.com/lora/v1/lockers/<sn>`

### URL Parameters

Parameter |Type | Description
--------- | -----------| -----------
sn |int | The SN of the parking locker to retrieve 



# 2.Parking sensors(Lora)

## 2.1 Get All Parking sensors

```shell
curl -X GET "http://device.api.parks8.com/lora/v1/sensors?offset=1&limit=10"
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

This endpoint retrieves all parking sensors.

### HTTP Request

`GET http://device.api.parks8.com/lora/v1/sensors?offset=1&limit=10`

### Query Parameters

| Parameter | Type | Description             |
| --------- | ---- | ----------------------- |
| offset    | int  | 1<=offset<(count/limit) |
| limit     | int  | 10<=limit<=100          |

### Response body detail

| Parameter    | type   | Description                    |
| ------------ | ------ | ------------------------------ |
| sn           | int    | 车位雷达SN                     |
| voltage      | float  | 电池电压，计量单位为毫安(mv)   |
| frequency    | float  | 线圈频率                       |
| car_detected | int    | 车辆检测状态(0:无车,1:有车)    |
| low_battery  | int    | 电池状态(0:正常,1:电量低)      |
| coil_fault   | int    | 线圈故障(0:正常,1:有故障)      |
| rs_si        | float  | 信号强度,趋于0上下表示信号较强 |
| updated_at   | string | 最后更新时间                   |



## 2.2 Get a Specific Parking sensor

```shell
curl -X GET "http://device.api.parks8.com/lora/v1/sensors/<sn>"
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

`GET http://device.api.parks8.com/lora/v1/sensors/<sn>`

### URL Parameters

| Parameter | Type | Description                              |
| --------- | ---- | ---------------------------------------- |
| sn        | int  | The sn of the parking sensor to retrieve |

### Response body detail

| Parameter    | type   | Description                    |
| ------------ | ------ | ------------------------------ |
| sn           | int    | 车位雷达SN                     |
| voltage      | float  | 电池电压，计量单位为毫安(mv)   |
| frequency    | float  | 线圈频率                       |
| car_detected | int    | 车辆检测状态(0:无车,1:有车)    |
| low_battery  | int    | 电池状态(0:正常,1:电量低)      |
| coil_fault   | int    | 线圈故障(0:正常,1:有故障)      |
| rs_si        | float  | 信号强度,趋于0上下表示信号较强 |
| updated_at   | string | 最后更新时间                   |



# 3. Subscribe notify

## 3.1 Set  notify 

```shell

curl -X POST "http://device.api.parks8.com/lora/v1/notifys"
```

> The above command request JSON structured like this:

```json
{
    "device_type": 38, 
    "status_changed_callback_url": "<your_callback_url>", 
    "commandResp_callback_url": "<your_callback_url>"
}
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
            "commandResp_callback_url":38.6
        }
    ]
}
```



### HTTP Request

`POST http://device.api.parks8.com/lora/v1/notifys`

### Request body detail

| Parameter                   | Type   | Description                                                  |
| --------------------------- | ------ | ------------------------------------------------------------ |
| device_type                 | int    | number 18 means parking locker,number 34 means parking sensor |
| status_changed_callback_url | string |                                                              |
| commandResp_callback_url    | string |                                                              |

## 3.2 Get callback url for notify 

```shell
curl -X GET "http://device.api.parks8.com/lora/v1/notifys?device_type=<18>"
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



### HTTP Request

`GET http://device.api.parks8.com/lora/v1/notifys?device_type=<18>`

### Query Parameters

| Parameter   | Type | Description                                                  |
| ----------- | ---- | ------------------------------------------------------------ |
| device_type | int  | number 18 means parking locker,number 34 means parking sensor |



# 4.Notify-parking locker(Lora)

## 4.1 Status changed

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

| Parameter          | type   | Description                    |
| ------------------ | ------ | ------------------------------ |
| sn                 | int    | 车位小锁SN                     |
| voltage            | float  | 电池电压，计量单位为毫安(mv)   |
| frequency          | float  | 线圈频率                       |
| locked             | int    | 锁状态(0:下锁,1:上锁)          |
| car_detected       | int    | 车辆检测(0：无车,1:有车)       |
| shell_opened       | int    | 外壳打开(0:正常,1:打开)        |
| low_battery        | int    | 电池状态(0:正常,1:电量低)      |
| coil_fault         | int    | 线圈故障(0:正常,1:有故障)      |
| bar_position_error | int    | 栏位置故障(0:正常,1:有故障)    |
| motor_fail         | int    | 电机故障(0:正常,1:有故障)      |
| rs_si              | float  | 信号强度,趋于0上下表示信号较强 |
| updated_at         | string | last update time               |
| sign               | string | signature string               |

## 4.2 Command changed

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

| Parameter      | type   | Description                                                 |
| -------------- | ------ | ----------------------------------------------------------- |
| guid           | string | guid                                                        |
| sn             | int    | SN of parking locker                                        |
| commnad_status | string | command state(sending=>pending=>arrived=>succeeded=>failed) |
| reason         | string | reason of failed                                            |
| updated_at     | string | last update time                                            |
| sign           | string | signature string                                            |

# 5.Notify-parking sensor(Lora)

## 5.1 Stauts changed

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

| Parameter    | type   | Description                    |
| ------------ | ------ | ------------------------------ |
| sn           | int    | 车位雷达SN                     |
| voltage      | float  | 电池电压，计量单位为毫安(mv)   |
| frequency    | float  | 线圈频率                       |
| car_detected | int    | 车辆检测状态(0:无车,1:有车)    |
| low_battery  | int    | 电池状态(0:正常,1:电量低)      |
| coil_fault   | int    | 线圈故障(0:正常,1:有故障)      |
| rs_si        | float  | 信号强度,趋于0上下表示信号较强 |
| updated_at   | string | last update time               |
| sign         | string | signature string               |

## 5.2 Command changed

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

| Parameter      | type   | Description                                                 |
| -------------- | ------ | ----------------------------------------------------------- |
| guid           | string | guid                                                        |
| sn             | int    | SN of parking sensor                                        |
| commnad_status | string | command state(sending=>pending=>arrived=>succeeded=>failed) |
| reason         | string | reason of failed                                            |
| updated_at     | string | last update time                                            |
| sign           | string | signature string                                            |

