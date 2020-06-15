# Pre-authorized order confirmation (receipt confirmation, order cancellation)

----

**URL/Path:**  

<table>
<td bgcolor=#F2F5A9>
/openApi/v1/orderconfirm
</td>
</table>

## Description

The e-commerce user confirms the receipt of the goods before generating a real transaction, and the transaction is accounted for.

## Request Header

| Content-Type|application/json|
| ---- | ---- |
|Method|POST|

## Request example

```json
{
    "transSerial": "NPPAY110663728270458881",
    "merchantId": 1777,
    "appId": 1777,
    "sign": "AE10DA321FC9761B45BCCB0D28DC6459",
    "thirdOrderId": "robot1592180459401",
    "orderStatus": 1,
    "remark": "",
    "version": "1.0",
    "timestamp": "1592180459401"
}
```

## Parameters

|Parameter|Required|Format|Description|
|:----    |:-------    |:--- |-- -|
|merchantId|M|N|Merchant ID|
|appId|M|N|Application ID | 
|merchantUserId|C|S| Merchant user unique number  |
| timestamp|M|S|Current timestamp millisecond | 
| version|M|S|API version | 
|sign|M|S|Signature  | 
|thirdOrderId|M|S|Merchant's unique order number (required)|
|orderStatus|M|N|Order result, 0 cancel order, 1 confirm receipt|
|transSerial| M |  S |NanoPay Payment order number|
|remark| O |  S |Remarks|

## Response Example

```json
{
    "code": 0,
    "data": {
        "orderAmount": 1,
        "transSerial": "NPPAY110663908877189121"
    },
    "message": "success",
    "sign": "AE10DA321FC9761B45BCCB0D28DC6459"
}
```

## Response parameter description

|Parameter | Required |Format |Description |
| ---- | ---- | ---- | ---- |
|    transSerial  |  M    | S | NanoPay Payment order number |
|  orderAmount    |   M   | N | orderAmount |

## Note

Idempotent is supported. If no return result is received after timeout, it can be called repeatedly.
