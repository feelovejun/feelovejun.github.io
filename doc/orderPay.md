# 发起付款接口

## 1. 接口地址：
    http://www.luobozhifu.cn/api/orderPay

## 2. 接口请求方式及参数：　
###  请求方式：POST
###  请求参数类型 : application/json

参数名称 | 参数类型 | 是否必需 | 说明 | 是否需要加密
---|---|---|---|---
sign | String | 是 | 接口加密签名，详细说明见：加密算法说明，==获取sign之后要做大写处理== | 否
userId | String | 是 | 商户账号 | 是
bus_order_no | String | 是 | 商户订单编号 | 是
money | Number | 是 | 订单金额（单位元） | 是
channel_type | String | 是 | 渠道类型：支付宝(Ali),微信(WxFixed)| 否
content | String | 否 | 商品描述 | 是
notify_url | String | 否 | 付款完成回调接口，如果为空则不通知 | 是
t | String | 否 | 时间戳 | 是

#### 请求签名规则

将接口参数按照key从小到大排序，过滤调用值为空的参数，并使用“&”拼接之后MD5加密，得到（大写）签名sign，加密字符串如下：

```
security&bus_order_no=val&content=val&money=val&notify_url=val&t=val&userId=val
```

###  返回参数说明
参数名称 | 参数类型  | 说明
---|---|---
code | int | 0为成功，1为失败
message | string | 接口处理结果信息
data | obj | 接口成功，会返回订单对象信息，详见data参数说明部分

####  data参数说明
参数名称 | 参数类型  | 说明
---|---|---
orderID | string | 系统订单id
orderNo | string | 系统订单编号
busOrderNo | string | 商户订单编号
money | float | 订单金额
realMoney | float | 实付金额
qrcode | String | base64二维码图片
qrcodeUrl | string | h5支付地址

### notify_url 成功支付后通知回调
#### 请求方式post
###### 当订单支付成功后会立即向你的服务器发起回调通知
#### 回调参数
参数名称 | 参数类型  | 说明
---|---|---
bus_order_no | String | 你系统的订单编号
id | String | 平台唯一标识
money | String | 订单金额
order_no | String |平台订单编号
pay_money | String | 用户支付金额
t | String | 时间戳
sign | String | 签名 签名MD5之后转大写

#### 回调签名规则
参数security&bus_order_no=val&id=val&money=val&order_no=val&pay_money=val&t=val按照这个顺序用“&”拼接之后MD5加密，得到（大写）签名sign
```

例子：F5BB2A45D2A613381E2712071704D731&bus_order_no=00033&id=6000000149617758&money=2.0&order_no=P201903120000021402&pay_money=2.0&t=1552406008936
```


# 3.其他说明

##### 萝卜支付签名加密，采用目前主流的接口签名加密方式

##### 加密需要的额外算法参数：平台商户创建时系统为每个商户生成的秘钥，该秘钥请商户妥善保管，切勿丢失或透漏给第三方。
