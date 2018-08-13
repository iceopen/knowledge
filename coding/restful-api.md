## RESTful API 设计指南
网络应用程序，分为前端和后端两个部分。当前的发展趋势，就是前端设备层出不穷（手机、平板、桌面电脑、其他专用设备......）。

参考地址：[RESTful API 设计指南](http://www.ruanyifeng.com/blog/2014/05/restful_api.html)

## 我们的规范
### 一、服务名称
每个微服务都需要提供一个服务名称，并且使用 service 结尾
> http://xxx/wechat-service/

### 二、版本号
版本号是区分，不同时间段的服务

> http://xxx/wechat-service/v1

### 三、接口功能区分

请求方法对应操作说明
```
GET（SELECT）：从服务器取出资源（一项或多项）。
POST（CREATE）：在服务器新建一个资源。
PUT（UPDATE）：在服务器更新资源（客户端提供改变后的完整资源）。
DELETE（DELETE）：从服务器删除资源。（不允许做物理删除，通过标示为进行软删除）
```

下面是一些例子。
```
GET /zoos：列出所有动物园
POST /zoos：新建一个动物园
GET /zoos/ID：获取某个指定动物园的信息
PUT /zoos/ID：更新某个指定动物园的信息（提供该动物园的全部信息）
DELETE /zoos/ID：删除某个动物园
GET /zoos/ID/animals：列出某个指定动物园的所有动物
DELETE /zoos/ID/animals/ID：删除某个指定动物园的指定动物
```

### 四、过滤信息（Filtering）
如果记录数量很多，服务器不可能都将它们返回给用户。API应该提供参数，过滤返回结果。
下面是一些常见的参数。

```
?limit=10：指定返回记录的数量
?offset=10：指定返回记录的开始位置。
?page=2&per_page=100：指定第几页，以及每页的记录数。
?sortby=name&order=asc：指定返回结果按照哪个属性排序，以及排序顺序。
?animal_type_id=1：指定筛选条件
```

### 五、返回 JSON 要求

- 1.命名：驼峰命名 小写开头，不可以使用特殊符号
    正确：code_err,codeErr
    错误：code*err,code%Err

- 2.层级：尽可能不超过三级
    正确：2级案例
        ```
            {
                "link": {
                    "rel": "collection https://www.example.com/zoos", 
                    "href": "https://api.example.com/zoos", 
                    "title": "List of zoos", 
                    "type": "application/vnd.yourformat+json"
                }
            }
        ```

错误：4级案例

```
           {
"resNum": 0,
"resMsg": "success",
"resData": {
    "m:MsgResponse": {
        "Head": {
            "ReplyID": "20170516131840",
            "ReplyModule": "gateway",
            "ErrDesc": "Success",
            "ErrCode": "00000000",
            "ReplyCommand": "QueryInvoice"
        },
        "@xmlns:m": "http://tempuri.org/TESTiam",
        "Body": {
            "Reseller": "0",
            "Count": "1",
            "PaymentMode": "现金",
            "InvoiceList": {
                "Invoice": {
                    "Status": "0",// 0:表示账单未支付，1:表示账单已支付
                    "BillType": "01",
                    "TotalAdj": "0",
                    "NewCharge": "20000",
                    "BalanceDue": "20000",//账单编号
                    "TotalPaid": "0",
                    "LateFeeAmount": "0",
                    "InvoiceNo": "185205752464",//账单编号
                    "FromDate": "2017-04-01",
                    "ToDate": "2017-04-30",
                    "BillDate": "2017-05-01"//账单日期
                }
            },
            "Result": "成功"
        	}
    	}
    }
}
```

- 3.返回规定：正常返回直接返回结构体，错误返回提供错误状态码和错误说明
    正确：
        ```
             {
                "link": {
                    "rel": "collection https://www.example.com/zoos", 
                    "href": "https://api.example.com/zoos", 
                    "title": "List of zoos", 
                    "type": "application/vnd.yourformat+json"
                }
            }
        ```
   错误：
     ```
             {
                "err_code": 200,
                "link": {
                    "rel": "collection https://www.example.com/zoos", 
                    "href": "https://api.example.com/zoos", 
                    "title": "List of zoos", 
                    "type": "application/vnd.yourformat+json"
                }
            }
        ```

- 4.GET 列表时候：必须提供当前页数、总页面、每页行数

