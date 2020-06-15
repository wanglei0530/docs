# Credit limit query

----

**URL/Path:**  

<table>
<td bgcolor=#F2F5A9>
/openApi/v1/creditquery
</td>
</table>

## Description

quota inquiry

## Request Header

| Content-Type|application/json|
| ---- | ---- |
|Method|POST|

## Request example

```json
{
    "merchantId": 1777,
    "appId": 1777,
    "mobile": "7999900079",
    "sign": "E5E3933D80B4D48CE96671DACB4C72E0",
    "merchantUserId": "78788",
    "version": "1.0",
    "timestamp": "1592180459328"
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
|mobile|C|S|Payer's Phone number(length:10) |

## Response Example

```json
{
    "code": 0,
    "data": {
        "merchantUserId": "78788",
        "mobile": "7999900079",
        "creditTotal": 1000,
        "creditRemain": 995,
        "status": 1,
        "activeStatus": 1
    },
    "message": "success",
    "sign": "58D828047F635F9BE30C20F0E099EC36"
}
```

## Note

Pass at least one of the two parameters merchantUserId, mobile.
