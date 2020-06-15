## 简介
待补充

## 接口规则
1. 接口请求头参数：CONTENT-TYPE = APPLICATION/JSON
2. 编码：UTF-8
3. 请求方式：POST BODY JSON格式
4. 签名算法：MD5

### 签名生成步骤如下: 

#### 第一步
设所有发送或者接收到的数据为集合M，将集合M内非空参数值的参数按照参数名ASCII码从小到大排序（字典序），使用URL键值对的格式（即key1=value1&key2=value2…）拼接成字符串stringA
>> 特别注意以下重要规则：
>> 1. 参数名ASCII码从小到大排序（字典序）；
>> 2. 如果参数的值为空不参与签名；
>> 3. 参数名区分大小写；
>> 4. sign参数不参与签名，将生成的签名与该sign值作校验。

#### 第二步
* 在stringA最后拼接上key得到stringSignTemp字符串，并对stringSignTemp进行MD5运算，再将得到的字符串所有字符转换为大写，得到sign值signValue。

#### 参数示例

假设传送的参数如下：
```json
{
  "appId":"1",
  "transSerial":"5daee677-4b3a-4e07-ad6c-118abaa36683",
  "merchantId":"5",
  "sign":"0219703722BC06F16519EB7504EC70F5",
  "timestamp":"7338470955",
  "version":"1.0"
}
```

##### 第一步：对参数按照key=value的格式，并按照参数名ASCII字典序排序如下：

```java
stringA = "appId=1&merchantId=5&timestamp=7338470955&transSerial=NPPAY123456789098&version=1.0";
```

##### 第二步：拼接API密钥：

```java
stringSignTemp = stringA + "&key=1"
sign = MD5(stringSignTemp).toUpperCase() = "E10ADC3949BA59ABBE56E057F20F883E"

// 最后生成的签名就是：E10ADC3949BA59ABBE56E057F20F883E
注：key为商户平台设置的密钥key
```

## 接口地址

* 测试环境API地址：https://api-test.nanopay.in.fg-example.com/
* 生产环境API地址：https://openapi.nanopay.in/

* 测试环境H5收银台地址：https://h5.nanopay.in.fg-example.com/h5sdk/home/index.html
* 生产环境H5收银台地址：https://h5.nanopay.in/h5sdk/home/index.html

* 测试环境激活及下载地址：https://h5.nanopay.in.fg-example.com/h5sdk/download/index.html
* 生产环境激活及下载地址：https://h5.nanopay.in/h5sdk/download/index.html

* 测试环境还款地址：https://h5.nanopay.in.fg-example.com/h5repayment/login/repayment.html?channel=2020888888
* 生产环境还款地址：https://h5.nanopay.in/repayment/login/repayment.html?channel=2020888888
  
## 测试参数
 
 | 字段说明 | 字段    | 获得方式 |
|-----------|-----------|-----------|
| 合作商户号 | merchantId|联系Nanopay获取 |
| 应用编号 | appId|联系Nanopay获取 |
| 商户秘钥 | key|联系Nanopay获取 |

> 开通测试商户号需商户提供ip地址

## 公共参数

|字段|类型|必须|默认值|注释|
|:----    |:-------    |:--- |-- -|------      |
|appId    |Long     |是 | 无 |     应用编号   |
|merchantId |Long |是 |   无 |   合作商户号  |
|sign     |String |是   |   无 |    签名     |
|timestamp |String |是   | 无  |   当前时间戳  |
|version |String |是   | 1.0  |  固定值1.0  |

> 必须上送，缺一不可! 

## 产品流程

待补充 

#### 支付流程：
1. 用户在商户APP选择nanopay支付。
2. 商户应该先生成订单，并用服务端调用nanopay预下单接口，获得交易流水号transSerial以及临时凭证tmpCode，tmpCode有效期跟订单有效期相同，且订单支付后失效。商户服务端把流水号及临时凭证返给商户的APP。
3. 商户APP带上流水号及临时凭证打开nanopay收银台h5页面进行支付。
例如测试环境为https://h5.nanopay.in.fg-example.com/h5sdk/home/index.html?tmpCode=openapi:tmpcode:4746f2f9987d4bac&transSerial=aaabbb
4. 商户提供回调接口，用户支付完成后，nanopay服务端会调用商户回调接口通知支付状态。
5. nanopay提供订单查询接口，商户也可主动查询订单状态。
6. 完成支付后，如何从nanopay的h5页面跳回到商户。需要商户提供一个跳转链接，我们跳过去的时候会带上两个参数，如https://aaa.com?result=success&thirdOrderId=833971122
如果支付失败result=fail

#### 页面激活流程：
1. 用户点击nanopay入口时商户APP应该先调用商户自己的服务端接口。
2. 商户服务端调用nanopay的获取临时凭证接口，获取临时凭证，并返给APP。
3. APP带上临时凭证，打开nanopay的激活页面。（例如测试环境为：https://h5.nanopay.in.fg-example.com/h5sdk/download/index.html?tmpCode=openapi:tmpcode:4746f2f9987d4bac）
4. 商户打开的webview应提供关闭按钮，激活后，用户可主动关闭商户APP的webview回到我的页面。
5. 商户不用判断用户是否已经激活，nanopay的页面会主动判断。

* 图待补充

