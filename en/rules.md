# Rules of API

----

* Request head parameter: Content-Type=application/json
* Code: UTF-8
* Request method: POST BODY JSON FORMAT
* Signature: MD5

## Steps for signature 
</br>

1. Set all request or response data as set M.
1. Sort the parameters of non-empty parameter values in set M from small to large according to the parameter name ASCII code (lexicographic order).
1. Use the format of URL key-value pairs (key1=value1&key2 =value2 ...) spliced into the stringA.
1. Append the key(application key) at the end of stringA to get the stringSignTemp.
1. Perform MD5 operation on stringSignTemp, then convert all the characters of the obtained string to stringSignTemp to get the signValue.

## Note 
</br>

* If the value of the parameter is empty, do not participate in the signature.
* Parameter names are case sensitive (Uppercase lowercase).
* The sign parameter does not participate in the signature, and the generated signature is checked against the sign value.

## Signature Example
</br>
Suppose the transmitted parameters are as follows:

```json
{
    "appId": "1",
    "transSerial": "5daee677-4b3a-4e07-ad6c-118abaa36683",
    "merchantId": 5,
    "sign": "0DCE5A089389111C30A2C105A9183543",
    "timestamp": "1588161191695",
    "version": "1.0"
}
```

> Step 1: Sort them according to the ASCII dictionary order of the parameter names Arrange the parameters in the format of key=value as follows:
```java
stringA="appId=1&merchantId=5&timestamp=1588161191695&transSerial=5daee677-4b3a-4e07-ad6c-118abaa36683&version=1.0";
```

> Step 2: Splicing the API key
```java
stringSignTemp=stringA+"&key=1";
signValue=MD5(stringSignTemp).toUpperCase()="0DCE5A089389111C30A2C105A9183543";
```

## Abbreviations 

|  Abbreviation    |  Description    |
| ---- | ---- |
|   C   |   Conditional   |
|   M   |   Mandatory   |
|   O   |   Optional   |
|   N   |   Numeric   |
|   S   |   String   |




