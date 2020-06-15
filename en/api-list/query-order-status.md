# Query order status

----


**URL/Path:**  

<table>
<td bgcolor=#F2F5A9>
/openApi/v1/orderquery 
</td>
</table>

## Description

Order Checking. If no NanoPay callback is received, the merchant can call this interface to check the order status.

## Request Header

|Method|POST|
| ---- | ---- |
| Content-Type|application/json|

## Request example

```json
{
    "appId": 1777,
    "transSerial": "NPPAY110663908877189121",
    "thirdOrderId": "",
    "merchantId": 1777,
    "sign": "E30C20F0E099EC3658D828047F635F9B",
    "timestamp": "1592180985471",
    "version": "1.0"
}
```

## Parameters

|Parameter|Required|Format|Description|
|:----    |:-------    |:--- |-- -|
|merchantId|M|N|Merchant ID|
|appId|M|N|Application ID | 
|timestamp|M|S|Current timestamp millisecond | 
|version|M|S|API version | 
|sign|M|S|Signature  | 
| thirdOrderId| M | S | Merchant's unique order number (required) |
| transSerial | M | S | NanoPay Payment order number |

## Response Example

```json
{
    "code": 0,
    "data": {
        "transSerial": "NPPAY110663908877189121",
        "transType": 1,
        "thirdMerchantId": 1777,
        "thirdOrderId": "THrobot1592180459401",
        "orderAmount": 1,
        "mobile": "7999900079",
        "transFee": 0.015,
        "transFeeAmt": 0.015,
        "goodsName": "hat",
        "goodsNum": 1,
        "goodsDetails": "hat",
        "refundStatus": 1,
        "refundAmount": 0,
        "expireTime": 1597328468727,
        "status": 2,
        "createTime": 1592180480950,
        "remark": ""
    },
    "message": "success",
    "sign": "0E099EC3658D828047F635F9BE30C20F"
}
```

## Response parameter description

|Parameter | Required |Format |Description |
| ---- | ---- | ---- | ---- |
|    transSerial  |  M    | S | NanoPay Payment order number |
|  tmpCode    |   M   | S | Temporary code |
|   transType   |    M    | N |  Transaction type: Transaction type: 1: consumption payment 2: payment refund, 7: pre-authorization, 8: pre-authorization refund |
|   thirdMerchantId   |  M    | N | Merchant ID |
|    thirdOrderId  |    M  |  S|  Merchant's unique order number (required)|
|  mobile    |    O  |  S| Payer's Phone number(length:10) |
|   orderAmount |  M    | N | Order amount (currently only supports Indian rupees) |
|   transFee   |   M   |  N|  Transaction fee rate, merchant fee rate at the time of order generation, unit: Rupee. 0.015 means 1.5%.|
|   transFeeAmt   |   M   |  N| The transaction fee is calculated based on the original amount. What the merchant needs to pay, due to t1 settlement, the refund handling fee will remain unchanged, and the handling fee in the refund transaction is a negative deduction, unit: Rupee |
|   goodsName   |   M   |  S| The name of the product purchased by the customer |
|   goodsDetails   |   O   | S |  Product details (length 512)|

## Note

 transSerial and thirdOrderId have at least one value. If there are two, transSerial shall prevail.