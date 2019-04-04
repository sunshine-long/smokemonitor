# 测试环境
```
通信协议：http
IP：uwonders.ticp.net
Port：5000
```
# 测试目的

测试烤烟过程中，相关数据推送，和紧急事件报警。
# APP相关功能和交互流程
### 常规交互流程
1.	登录APP，进入主页
2.	获取烤烟历史消息列表，
3.	点击列表中任意一项，查看交互流程
### 消息推送交互流程
1.	收到推送消息（或报警），
2.	点击消息（或报警），判断此时是否登录过期；
3.  过期，跳转到登录页面，先登录，登录成功，跳转到消息（或报警）详情页；
4.  未过期，直接跳转到消息（或报警）详情页。

# 接口
## 登录
### 描述：
用于用户登录，完成稿后并绑定推送ID，用于定向推送消息。
### API：
`"/user/login"`
### 请求方式：
`POST`
#### 请求参数

名称（name） | 类型（Type）| 说明 
---|---|---
userName | String | 用户名
password | String | 密码（加密）
#### 请求示例(Request)
```
{
	"userName": "marlon",
	"password": "123456"   //加密
}
```
#### 返回参数
名称（name） | 类型（Type）| 说明 
---|---|---
userName | String | 用户名
password | String | 密码（加密）
avatar   | String | 头像
token    | String | 鉴权标识
userID   | long | 用户ID
mobile   | String | 手机号
realName | String | 用户真实姓名（若实名）
idCard   | String | 身份证号码（若实名）
#### 返回示例（Response）
`成功时：`
```
{
    "code": 200,
	"msg": "success",
	"data": {
	    "userName":"marlon",
	    "password":"dkfhdklflkas15dfdjmfl",
	    "avatar":null,
	    "token":"jdfidjfsdkfeiepwers55df4",
	    "userID":"1",
	    "mobile":null,
	    "realName":null,
	    "idCard":null
	}
}
```
`失败时：`
```
{
    "code": 非200,
	"msg": "错误提示信息",
	"data":null //返回null 或者不返回
}
```
# 获取消息列表
### 描述：
获取消息列表信息
### API:
`"/monitor/query"`
### 请求方式：
`POST`
### 请求参数
名称（name） | 类型（Type）| 说明 
---|---|---
token | String | 用户登录标识
terminal_id | String | 烤房批次
batch_number | String | 烤房编号
### 请求示例（Request）：
```
{
"token":"dhsfjshfdhsjdfhjdsfh",
"terminal_id":"uwonders",
"batch_number":"10000061"
}
```
### 返回参数
名称（name） | 类型（Type）| 说明 
---|---|---
start_time | String | 开始时间
list | Array | 消息列表
time | String | 当前图片时间
id | String | 图片的id
image_url | String | 图片url
dry_bulb_temperature | String | 当前干球温度
web_bulb_temperature | String | 当前湿球温度
submit_time | String | 提交时间
### 返回示例（Response）：
`成功时：`
```
{
	"code": 200,
	"msg": "success",
	"data":
	    "start_time":"2018-10-24 10:38:44",
	    "list":[{
		    "time": "2018-10-24 10:38:44",
	    	"dry_bulb_temperature": "60C°",
	    	"web_bulb_temperature": "30C°",
	    	"id": "1000001",
	    	"image_url": "http://www.hao123.com/redian/sheshouyef.htm",
	    	"submit_time": "2018-10-24 08:38:44"
	    }, {
	    	"time": "2018-10-24 10:38:44",
	    	"dry_bulb_temperature": "60C°",
	    	"web_bulb_temperature": "30C°",
	    	"id": "1000002",
	    	"image_url": "http://www.hao123.com/redian/sheshouyef.htm",
	    	"submit_time": "2018-10-24 08:38:44"
	    }, {
	        "time": "2018-10-24 10:38:44",
	    	"dry_bulb_temperature": "60C°",
	    	"web_bulb_temperature": "30C°",
	    	"id": "1000003",
	    	"image_url": "http://www.hao123.com/redian/sheshouyef.htm",
	    	"submit_time": "2018-10-24 08:38:44"
    	}]
}
```
`失败时：`
```
{
    "code": 非200,
	"msg": "错误提示信息",
	"data":null //返回null 或者不返回
}
```
# 消息详情
### 描述：
用于获取消息详情信息
### API:
`"/monitor/query/id"`
### 请求方式：
`POST`
### 请求参数：
名称（name） | 类型（Type）| 说明 
---|---|---
token | String | 用户登录标识
monitor_id | String | 图片对应点ID
### 请求示例（Request）：
```
{
	"token:"dhsfjshfdhsjdfhjdsfh",
	"monitor_id":"121"
}
```
### 返回参数
名称（name） | 类型（Type）| 说明 
---|---|---
start_time | String | 开始时间
list | Array | 消息列表
time | String | 当前图片时间
id | String | 图片的id
image_url | String | 图片url
dry_bulb_temperature | String | 当前干球温度
web_bulb_temperature | String | 当前湿球温度
submit_time | String | 提交时间
### 返回示例（Response）：
`成功时：`
```
{
	"code": 200,
	"msg": "success",
	"data":
	    "start_time":"2018-10-24 10:38:44",
	    "list":[{
		    "time": "2018-10-24 10:38:44",
	    	"dry_bulb_temperature": "60C°",
	    	"web_bulb_temperature": "30C°",
	    	"id": "1000001",
	    	"image_url": "http://www.hao123.com/redian/sheshouyef.htm",
	    	"submit_time": "2018-10-24 08:38:44"
	    }]
}
```
`失败时：`
```
{
    "code": 非200,
	"msg": "错误提示信息",
	"data":null //返回null 或者不返回
}
```
# 发送获取图片请求
### 描述：
发送获取最新图片信息请求
### API:
`"/push/take_photo"`
### 请求方式：
`POST`
### 请求参数
名称（name） | 类型（Type）| 说明 
---|---|---
token | String | 用户登录标识
terminal_id | String | 烤房批次
batch_number | String | 烤房编号
### 请求示例（Request）：
```
{
"token":"dhsfjshfdhsjdfhjdsfh",
"terminal_id":"uwonders",
"batch_number":"10000061"
}
```
### 返回参数
`null`
### 返回示例（Response）：
`成功时：`
```
{
    "code": 200,
	"msg": "sccuess",
	"data":null //返回null 或者不返回
}
```
`失败时：`
```
{
    "code": 非200,
	"msg": "错误提示信息",
	"data":null //返回null 或者不返回
}
```
# 查询所有烤房和批次
### 描述：
查询所有烤房和批次
### API:
`"/monitor/query/terminal_account_and_batch_number"`
### 请求方式：
`POST`
### 请求参数
名称（name） | 类型（Type）| 说明 
---|---|---
token | String | 用户登录标识
### 请求示例（Request）：
```
{
    "token:"dhsfjshfdhsjdfhjdsfh"
}
```
### 返回参数
名称（name） | 类型（Type）| 说明 
---|---|---
terminal_id | String | 烤房批次
batch_number | String | 烤房编号
### 返回示例（Response）：
`成功时：`
```
{
    "code": 200,
	"msg": "sccuess",
	"data":[{
	    "terminal_id":"uwonders",
	    "batch_number":"10000060"
	},{
	    "terminal_id":"uwonders",
	    "batch_number":"10000061"
	},{
	    "terminal_id":"uwonders",
	    "batch_number":"10000062"
	},{
	    "terminal_id":"uwonders",
	    "batch_number":"10000063"
	}]
}
```
`失败时：`
```
{
    "code": 非200,
	"msg": "错误提示信息",
	"data":null //返回null 或者不返回
}
```
# 查询温度曲线
### 描述：
查询当前烤房/批次的温度曲线
### API:
`"/monitor/query/terminal_account_and_batch_number"`
### 请求方式：
`POST`
### 请求参数
名称（name） | 类型（Type）| 说明 
---|---|---
token | String | 用户登录标识
terminal_id | String | 烤房批次
batch_number | String | 烤房编号
### 请求示例（Request）：
```
{
    "token":"dhsfjshfdhsjdfhjdsfh",
    "terminal_id":"uwonders",
    "batch_number":"10000061"
}
```
### 返回参数
名称（name） | 类型（Type）| 说明 
---|---|---
terminal_id | String | 烤房批次
batch_number | String | 烤房编号
temperature_setting | Arrqy | 温度曲线时间列表
temp | String | 干球温度
time | String | 烘烤时间
### 返回示例（Response）：
`成功时：`
```
{
    "code": 200,
	"msg": "sccuess",
	"data":
	"temperature_setting":[{
	   "temp": 0,
	   "time": 0
	    },{
	   "temp": 34,
	   "time": 10
	},{
	   "temp": 34,
	   "time": 20
	},{
	    "temp": 34,
	    "time": 40
	}]
}
```
`失败时：`
```
{
    "code": 非200,
	"msg": "错误提示信息",
	"data":null //返回null 或者不返回
}
```
# 设置温度曲线
### 描述：
设置当前烤房/批次的温度曲线
### API:
`"/push/set_temperature"`
### 请求方式：
`POST`
### 请求参数
名称（name） | 类型（Type）| 说明 
---|---|---
token | String | 用户登录标识
terminal_id | String | 烤房批次
dry_bulb_temperature | String | 设置干球温度
dry_bulb_temperature_duration | String | 设置烘烤时间
time | String | 开始烘烤时间点
### 请求示例（Request）：
```
{
    "token":"dhsfjshfdhsjdfhjdsfh",
    "terminal_id":"uwonders",
    "batch_number":"10000061"
    "dry_bulb_temperature:"80",
    "dry_bulb_temperature_duration":"20",
    "time":"15"
}
```
### 返回参数
`null`
### 返回示例（Response）：
`成功时：`
```
{
    "code": 200,
	"msg": "success",
	"data":null //返回null 或者不返回
}
```
`失败时：`
```
{
    "code": 非200,
	"msg": "错误提示信息",
	"data":null //返回null 或者不返回
}
```
