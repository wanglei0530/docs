# Pre order

----

**URL/Path:**  

<table>
<td bgcolor=#F2F5A9>
/openApi/v1/ordercreate 
</td>
</table>

## Description

Merchant server calls NanoPay pre-order interface  to get the transSerial number of NanoPay and tmpCode. 
The merchant app/web then brings these two parameters to open NanoPay payment page. (The address of the payment page after putting in the parameters is like: 

```html
https://h5.nanopay.in.fg-example.com/h5sdk/home/index.html?tmpCode=openapi:tmpcode:4746f2f9987d4bac&transSerial=aaabbb)
```

## Request Header

|Method|POST|
| ---- | ---- |
| Content-Type|application/json|

## Request example

```json
{
    "mobile": "7999900079",
    "sign": "8821D6940915EDC0F2844A88A3629236",
    "version": "1.0",
    "orderAmount": 1.26,
    "expireTime": 1800,
    "transType": 7,
    "merchantId": 1777,
    "merchantName": "test merchant",
    "appId": 1777,
    "thirdOrderId": "ro1592180459401",
    "merchantUserId": "78788",
    "payeeMerchantId": "1121",
    "payeeMerchantName": "Mi-Home",
    "goodsName": "hat",
    "goodsDetails": "hat",
    "goodsNum": 1,
    "timestamp": "1592180459401"
}
```

## Parameters

|Parameter|Required|Format|Description|
|:----    |:-------    |:--- |-- -|
|merchantId|M|N|Merchant ID|
|appId|M|N|Application ID | 
|merchantUserId|C|S| Merchant user unique number  |
|timestamp|M|S|Current timestamp millisecond | 
|version|M|S|API version | 
|sign|M|S|Signature  | 
|mobile|C|S|Payer's Phone number(length:10) |
| merchantName | O | S | Partner merchant name (nanopay distribution) |
| thirdOrderId| M | S | Merchant's unique order number (required) |
| payeeMerchantId | O | S | Actual collection merchant id (the merchant of the partner merchant) |
| payeeMerchantName | O | S | The name of the actual payment merchant (the merchant of the partner merchant) |
| orderAmount | M | N | Order amount (currently only supports Indian rupees) |
| transType | M | N | Transaction type: 1 consumer payment (in-app payment), 7 pre-authorization |
| goodsName | M | N | The name of the product purchased by the customer |
| goodsDetails | O | S | Product details (length 512) |
| goodsNum | O | N | Number of Products |
| expireTime | O | N | Order validity period, also tmpCode validity period (in seconds), default 1800 seconds|

## Response Example

```json
{
    "code": 0,
    "data": {
        "transSerial": "NPPAY110663728270458881",
        "tmpCode": "openapi:tmpcode:28e7ac1c2d5a44a3"
    },
    "message": "success",
    "sign": "8821D6940915EDC0F2844A88A3629236"
}
```

## Response parameter description

|Parameter | Required |Format |Description |
| ---- | ---- | ---- | ---- |
|    transSerial  |  M    | S | NanoPay Payment order number |
|  tmpCode    |   M   | S | Temporary code |



## Note

null
