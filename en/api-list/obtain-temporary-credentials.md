# Obtain temporary credentials

----

**URL/Path:**  

<table>
<td bgcolor=#F2F5A9>
/openApi/v1/tmpcode  
</td>
</table>

## Description

Obtain temporary credentials, which are only used to open the activation page provided by NanoPay. Valid within 5 minutes

## Request Header

|Method|POST|
| ---- | ---- |
| Content-Type|application/json|

## Request example

```json
{
    "merchantUserId": "78788",
    "mobile": "9811039269",
    "merchantId": 1777,
    "appId": 1777,
    "timestamp": "1577158821943",
    "version": "1.0",
    "sign": "3F329ECF080D561C3DB012931E394750"
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

## Response Example

```json
{
    "code": 0,
    "data": {
        "tmpCode": "openapi:tmpcode:66c097cfbbf84ae5",
        "merchantUserId": "78788"
    },
    "message": "success",
    "sign": "3F329ECF080D561C3DB012931E394740"
}
```

## Response parameter description

|Parameter | Required |Format |Description |
| ---- | ---- | ---- | ---- |
|    merchantId  |  M    | N | UserId of request parameter |
|  tmpCode    |   M   | S | Temporary code |



## Note

tmpCode is valid for 5 minutes.

