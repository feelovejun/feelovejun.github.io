# 订单查询接口

#### 1. 接口地址：
    http://www.luobozhifu.cn/api/orderInfoByNo

#### 2. 接口请求方式及参数：
请求方式：POST

参数名称 | 参数类型 | 是否必需 | 说明 | 是否加密
---|---|---|---|---
sign | String | 是 | 接口加密签名，详细说明见：加密算法说明 | 否
userId | String | 是 | 商户账号 | 是
bus_order_no | String | 是 | 商户订单编号 | 是
t | String | 否 | 时间戳 | 是

#### 3. 接口返回参数类型及内容：
返回参数类型：application/json

参数内容：

{

    "code" : 0 ,

    "message": "",

    "data":{

        "id":"订单编号",

        "channelID":"渠道id",

        "busOderNo":"商户订单编号",

        "orderNo":"平台订单编号",

        "goodsName":"商品名称",

        "money": 20.00,

        "realMoney": 20.00,

        "status": 0,

        "finishTime": "订单完成时间，格式yyyy-MM-dd HH:mm:ss"

    }

}

字段说明：
code:0成功，1失败

money：订单金额

realMoney: 订单实付金额

status: 0表示未支付，1付款成功
