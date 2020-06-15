# Asynchronous notification of refund result

----


**URL/Path:**  

<table>
<td bgcolor=#F2F5A9>
Merchant apply
</td>
</table>

## Description

refund result , Nanopay call merchant 

## Request Header

|Method|POST|
| ---- | ---- |
| Content-Type|application/json|

## Request example

```json
{
    "createTime": 1592177723565,
    "expireTime": 1594769723000,
    "refundAmount": 0.26,
    "settlementStatus": 1,
    "status": 2,
    "thirdMerchantId": 1777,
    "thirdOrderId": "ro1592177723547",
    "transSerial": "NPPAY110640778168598530",
    "transType": 2,
    "sign": "2D27C90FCCC519B46B021008F6D6BF67"
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
|   refundAmount |  M    | N | Refund order amount (currently only supports Indian rupees) |
| expireTime | M  |  N | expireTime .Number of milliseconds since January 1, 1970 |
| status | M  |   N| Order status. 1: initial, 2: transaction success, 3: transaction failure 4：expired ,5:deemed,6: cancel  |
|createTime  | M  |  N | Timestamp .Number of milliseconds since January 1, 1970 |

## Remarks

After receiving the asynchronous notification, the refunding party will return to **"SUCCESS".**

* If SUCCESS is not received, the notification will be repeated 8 times. Interval time (1, 5, 10, 30, 60, 120, 240) Unit: minutes

**Special reminder:**

1. The merchant system must perform signature verification on the content of the payment result notification, and verify whether the returned order amount is consistent with the order amount on the merchant side, to prevent data leakage resulting in "false notice" and loss of funds. 

1. When receiving a notification for processing, first check the status of the corresponding business data to determine whether the notification has been processed. If it has not been processed, then process it again. If processed, return the result directly. Before performing status checking and processing on business data, data locks should be used for concurrency control to avoid data confusion caused by function re-entry.

