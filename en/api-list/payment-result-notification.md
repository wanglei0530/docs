# Payment result notification

----

**URL/Path:**  

<table>
<td bgcolor=#F2F5A9>
Merchant apply
</td>
</table>

## Description

Payment result notification. Nanopay call merchant 

## Request Header

| Content-Type|application/json|
| ---- | ---- |
|Method|POST|

## Request example

```json
{
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
}
```

## Parameters

|Parameter | Required |Format |Description |
| ---- | ---- | ---- | ---- |
|    transSerial  |  M    | S | NanoPay Payment order number |
|   transType   |    M    | N |  Transaction type: Transaction type: 1: consumption payment 2: payment refund, 7: pre-authorization, 8: pre-authorization refund |
|   thirdMerchantId   |  M    | N | Merchant ID |
|    thirdOrderId  |    M  |  S|  Merchant's unique order number (required)|
|  mobile    |    O  |  S| Payer's Phone number(length:10) |
|   orderAmount |  M    | N | Order amount (currently only supports Indian rupees) |
|   transFee   |   M   |  N|  Transaction fee rate, merchant fee rate at the time of order generation, unit: Rupee. 0.015 means 1.5%.|
|   transFeeAmt   |   M   |  N| The transaction fee is calculated based on the original amount. What the merchant needs to pay, due to t1 settlement, the refund handling fee will remain unchanged, and the handling fee in the refund transaction is a negative deduction, unit: Rupee |
|   goodsName   |   M   |  S| The name of the product purchased by the customer |
|   goodsDetails   |   O   | S |  Product details (length 512)|
| goodsNum   |  M |  N |  Number of Products |
| refundStatus |  M | N  | 1: There are refunds, 2: No refunds. Refund failure is also 2. If this a refund order this will be 2. |
|  refundAmount|  M |  N |  Refund amount, unit: Rupee(partial refunds are not supported yet). If this a refund order this will be 0. |
| expireTime | M  |  N | expireTime .Number of milliseconds since January 1, 1970 |
| status | M  |   N| Order status. 1: initial, 2: transaction success, 3: transaction failure 4：expired ,5:deemed,6: cancel  |
|createTime  | M  |  N | Timestamp .Number of milliseconds since January 1, 1970 |
| remark |  O |  N |  Remark |

## Remarks

After receiving the asynchronous notification, the payment initiator returns **"SUCCESS"**

* If SUCCESS is not received, the notification will be repeated 8 times. Interval time (1, 5, 10, 30, 60, 120, 240) Unit: minutes

**Special reminder:**

1. The merchant system must perform signature verification on the content of the payment result notification, and verify whether the returned order amount is consistent with the order amount on the merchant side, to prevent data leakage resulting in "false notice" and loss of funds. 

2. When receiving a notification for processing, first check the status of the corresponding business data to determine whether the notification has been processed. If it has not been processed, then process it again. If processed, return the result directly. Before performing status checking and processing on business data, data locks should be used for concurrency control to avoid data confusion caused by function reentry.
