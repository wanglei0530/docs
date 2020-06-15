# Public Parameters & Response Code

----

## Public parameters

|Parameter|Required|Format|Description|
|:----    |:-------    |:--- |-- -|
|merchantId|M|N|Merchant ID|
|appId|M|N|Application ID | 
| timestamp|M|S|Current timestamp millisecond | 
| version|M|S|API version | 
|sign|M|S|Signature  | 

## Request Response Code:

```text
0: success
4000: Business Parameter Error
4001: Interface Not Present
4002: Signature Error
4003: Merchant Not Present
4004: Order Not Present
4005: Application Not Present
4006: Merchant Application Not Matching
4007: Merchant Not Whitelisted or Not Active                
710001: nonexistent orders 
710002: merchant does not exist
710003: wrong of order amount 
710006: nonexistent orders 
710007: the order already completed 
710010: the order does not exist
710011: orders cannot be refunded
710012: the order has been refunded
710014: can‘t repeat order
710015: pre order fail 
710017: parameters are missing 
710018: check signature fail 
710020: no relevant data was obtained 
710021: order closed
710022: order expired
710023: original order does not exist
710024: refund order exists
710025: refundAmount Incorrect format
710026: sum refundAmount is greater than orderAmount
710027: order cancellation
710028: order processing                
790001: resource not found
790002: request error
790004: parameter error
790003: network error
790005: operation fail
790006: refuse operate                
790001: resource not found
790002: request error
790003: network error
790004: parameter error
790005: operation fail
790006: refuse operate
```