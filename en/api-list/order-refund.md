# Order refund

----

**URL/Path:**  

<table>
<td bgcolor=#F2F5A9>
/openApi/v1/orderrefund 
</td>
</table>

## Description

Apply for refund

## Request Header

|Method|POST|
| ---- | ---- |
| Content-Type|application/json|

## Request example

```json
{
    "refundType": 1,
    "transSerial": "NPPAY110663908877189121",
    "merchantId": 1777,
    "thirdRefundId": "rf1592180483330",
    "appId": 1777,
    "sign": "9B46B021008F6D6BF672D27C90FCCC51",
    "version": "1.0",
    "timestamp": "1592180483330",
    "refundAmount": 0.26
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
|thirdRefundId|M|S|Merchant's unique refund order number  |
| refundType | M | N | Refund types: 1 refund for transaction orders, 2 refund for pre-authorized orders |
| refundAmount| M | N | Refund amount|
| transSerial | M | S | NanoPay Payment order number |

## Response Example

```json
{
    "code": 0,
    "data": null,
    "message": "success",
    "sign": "9B46B021008F6D6BF672D27C90FCCC51"
}
```

## Note

about transSerial

* When refundType is 1. pass transSerial which is returned by Pre-order API.
* When refundType is 2. pass new transSerial which is returned by Pre-authorized order confirmation API.
