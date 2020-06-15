# Response example

----

## Example of success

```json
{
    "code": 0,
    "data": {
        "transSerial": "NPPAY90583190755278850",
        "transType": 1,
        "thirdMerchantId": 2020000802,
        "thirdOrderId": "263354547209",
        "orderAmount": 100,
        "mobile": "9811039269",
        "transFee": 0.01,
        "transFeeAmt": 1.5,
        "goodsName": "hat",
        "goodsNum": 1,
        "goodsDetails": "hat",
        "refundStatus": 2,
        "refundAmount": 0,
        "expireTime": 1590675560815,
        "status": 2,
        "createTime": 1589786672815,
        "remark": ""
    },
    "message": "success",
    "sign": "7AD007BFB15BD6AD1FEBA60A15948388"
}
```

## Example of exceptions

```json
{
    "code": 4006,
    "data": null,
    "message": "app merchant mismatching",
    "sign": null
}
```