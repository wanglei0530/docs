# Payment Flow

----

## Flow Chart

![1](https://tva1.sinaimg.cn/large/007S8ZIlly1gftf2xxyjkj30u00z975t.jpg)

## Technical integrate flow

* Merchant call **[Credit limit query API](en/api-list/credit-limit-query)** with merchant user id or mobile number to get user wallet status and credit.

* Customer choose NanoPay to pay. Merchant create order first and then call NanoPay **[Pre-order API](en/api-list/pre-order)** to create order. NanoPay return **transSerial** and **tmpCode** real time.
</br>

**Note:** The validity period of tmpCode is the same as the order validity period.

* Open (or redirect to) **NanoPay payment page** with **transSerial** and **tmpCode.**

* The merchant needs to provide a **return URL**. When customer click ‘Return’ button after completing the payment on NanoPay payment page, it will jump back to the merchant. When jump over, it will bring two parameters: result and **thirdOrderId**. Such as: https://XXXXXXX.com?result=success&thirdOrderId=833971122. If the payment fails result=fail, **thirdOrderId** is merchant order id which is passed by Pre-order API.

* The merchant need provides a **[callback API](en/api-list/payment-result-notification)**. After customer completes the payment, the NanoPay server will call the merchant callback API to inform the payment status.

* Nanopay provides an query **[order status API](en/api-list/query-order-status)** and merchants can also actively query the order status.

* If customer initiates a refund, Merchant create refund order first and then call NanoPay **[order refund API](en/api-list/order-refund)** to create refund order.

* After the refund is completed, NanoPay server will call the merchant **[refund callback API](en/api-list/asynnotify-refundresult)** to inform the refund status. So, the merchant need provides a refund callback API.
