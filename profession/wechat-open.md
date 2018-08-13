# 微厅开放平台

## 获取AccessToken
地址：http://m.sh.189.cn/service/1.0/access/token?appid=APPID&secret=SECRET     

发送方式：GET

返回数据：
```
{
  "data": "=jLdmlnLUyr-BzKfriqsMEr3X9=rRjrtSln9ryLcH",
  "status": 200,
  "info": 0
}
```
> 说明：获取accesstoken 接口每天调用次数有限，不能无限制调用，accesstoken 有效期为7200s，请存储定时维护。

## 微信基本授权
地址：http://m.sh.189.cn/service/wxoauth/2.0/getBaseUrl?access_token=ACCESS_TOKEN 

发送方式：POST

请求参数：
- state（授权url）

返回参数：
```
{
    "status": 200,
    "redirect": "https://open.weixin.qq.com/connect/oauth2/authorize?appid=wx1b0d10b65d395395&redirect_uri=http%3A%2F%2Fm.sh.189.cn%2Fservice%2Fwxoauth%2F2.0%2Fwxcode&response_type=code&scope=snsapi_base&state=http%3A%2F%2Fm.sh.189.cn%2Fservice%2Fwxoauth%2F2.0%2Findex#wechat_redirect"
}
```

说明：重定向返回参数redirect，code 将会被携带在授权url（state）参数中返回
例如：请求参数state（http://m.sh.189.cn/service/wxoauth/2.0/index）
重定向redirect结果：
http://m.sh.189.cn/service/wxoauth/2.0/index?code=NTc1ZmFmNGIwODYxM2U3YjZkOTE3ZWUz


## 获取openid
地址：http://m.sh.189.cn/service/wxoauth/2.0/getOpenidByCode?access_token=ACCESS_TOKEN   

发送方式：post

请求参数：
- code
返回成功数据：
```
{
    "status": 200,
    "openid": ""
}
```
返回失败数据：
```
{
    "status": 40005,
    "errMsg": "code 已过期"
}
```

## 通过OPENID 获取微信绑定 户信息
通过 OPENID 获取微信绑定 户信息，是 户在微厅中绑定的设备信息和 户信息

地址：GET

返回数据:
```
{
    "result":{
        "_id":"57eb5210e4dace7558b81421",
        "openid":"oKXUCj1Fp4fNnb99liSkslcM_D-X",
        "nickname":"xx",
        "headimg":"http://wx.qlogo.cn/mmopen/STan0NGQK3G1h-BxcZXdx7xGEpAcmYCUy3GgK1lQv399IiaLvxg7g1OAA8VK- MVRt0SPxXAh0Q0iaq86CWw7Tw22pg/0",
        "__v":0,
        "updateAt":"2016-09-28T05:16:00.804Z",
        "createAt":"2016-09-28T05:16:00.804Z",
        "accounts":[
            {
                "deviceno":"62306600",
                "devicename":"固话",
                "bindtime":"2016-05-27 11:04:36",
                "bindtdate":"2016-05-27 11:04:36",
                "bpn":"92125567729",
                "sort":"1"
            },
            {
                "sort":"1"
            },
            {
                "deviceno":"18964524000",
                "devicename":" 机",
                "bindtime":"2016-01-21 08:48:53",
                "bindtdate":"2016-01-21 08:48:53",
                "bpn":"82537753581",
                "sort":"1"
            },
            {
                "sort":"1"
            },
            {
                "deviceno":"62062100",
                "devicename":"固话",
                "bindtime":"2016-05-27 10:47:57",
                "bindtdate":"2016-05-27 10:47:57",
                "bpn":"72397130079",
                "sort":"1"
            }
        ]
    },
    "flag":0
}
```

## 中奖结果通知模板接口
地址：http://m.sh.189.cn/service/1.0/sendPrizeNotice?access_token=ACCESS_TOKEN  

发送方式：POST
```
请求参数
openid       openid 
first            中奖描述
activity       活动名称
prize          奖品
remark       备注
url             模板链接url地址
```
返回数据：
```
{
    status: 200,
    result: "发送成功"
}
```
```
{
    status: 0,
    result: "发送失败"
}
```
```
{
    status: 40005,
    errMsg: "推送接口异常"
}
```

例子：
```

First Header | Second Header 
:----------- | :-----------: 
openid       | openid      
first        | 亲爱的老司机，您的游戏积分已经排在全国前十名。        
activity     | 老司机大比拼  
prize        | 限量精美玩偶一个
remark       | 获奖者：17717500243
url          | 模板链接url地址
```

![pushdemo](img/1.1.png)

## 爱流量回传登录状态
地址：http://m.sh.189.cn/service/weekBind/create?access_token=ACCESS_TOKEN  

发送方式：POST

请求参数
```
{
    "openid": "微信唯一标识 非空",
    "deviceno": "设备号 非空",
    "operators": "运营商 可选",
    "qcellcore": "归属地 可选",
    "channel": "1",
    "from": "love flow"
}
```
返回正常数据：
```
{"data":"success","status":200,"info":0}
```

返回异常数据：
```
{“data":"错误信息","status":0,"info":0}
```

## 爱流量回传订购业务
地址：http://m.sh.189.cn/service/flowOrders/create?access_token=ACCESS_TOKEN  

发送方式：POST

请求参数
```
{
    "openid": "微信唯一标识 必传",
    "deviceno": "设备号 必传",
    "traffic_package_name": "流量包名称 必传",
    "transaction_date": "交易日期 可选",
    "channel": "1",
    "from": "love flow"
}
```

返回正常数据：
```
{“data":"订单号","status":200,"info":0}
```

返回异常数据：
```
{"data":"错误信息","status":0,"info":0}
```

## APP快速入口
地址：http://m.sh.189.cn/service/appOauthen/Ticket?access_token=ACCESS_TOKEN  

发送方式：GET

请求参数：ticket
返回正常数据：
```
{
    "errcode": 0,
    "data": {
        "mobile": "17717463317"
    }
}
```
返回异常数据：
```
{
    "status": 0,
    "errMsg": "access_token校验异常"
}
```
```
{
    "status": 40005,
    "errMsg": "接口异常，请稍后再试"
}
```
```
{
    "errcode": 1,
    "data": {
        "mobile": "ticket必须给出"
    }
}
```
```
{
    "errcode": 1,
    "data": "手机号码获取异常",
    "msg": {
        "CAPRoot": {
            "SessionHeader": [
                {
                    "TransactionID": [
                        "3599901201610144084678881"
                    ],
                    "ActionCode": [
                        "1"
                    ],
                    "RspTime": [
                        "20161014084034"
                    ],
                    "Response": [
                        {
                            "RspType": [
                                "1"
                            ],
                            "RspCode": [
                                "1992"
                            ],
                            "RspDesc": [
                                "根据ticket查询网站注册用户信息为空!"
                            ]
                        }
                    ]
                }
            ]
        }
    }
}
```
