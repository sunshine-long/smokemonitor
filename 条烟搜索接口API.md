
# 测试环境
```
通信协议：http
IP：192.168.0.103（暂定）
Port：8088（暂定）
```
# 测试目的

1.搜索条烟的种类，查询条烟的相关信息（包括：烟名，条码，编码，图片样式等信息）;
2.注册新的条烟种类

# 相关类
```
SmokeModel {
    //id 数据库存储的id
    private String id;
    // 烟名
    private String smokeName;
    // 烟条码
    private String smokeBarCode;
    // 烟编码
    private String smokeCoding;
    // 图片的url 
    private List<String> images;
    }
 ```
 
 ```
 Userinfo {
    //用户名
    private String username;
    //密码
    private String passwords;
    //头像
    private String avatar;
    //token
    private String token;
    //用户ID
    private long userID;
    //电话
    private String mobile;
    //真实姓名
    private String realName;
    //身份证号码
    private String idCard;
    }
 ```
# 接口
### 登录
#### 请求方法
`POST`
#### API 
```
"user/login"
```
#### 请求参数

名称（name） | 类型（Type）| 说明 
---|---|---
userName | String | 用户名
password | String | 密码（MD5加密）

#### 返回参数
名称（name） | 类型（Type）| 说明 
---|---|---
userName | String | 用户名
password | String | 密码（MD5加密）
avatar   | String | 头像
token    | String | 鉴权标识
userID   | long | 用户ID
mobile   | String | 手机号
realName | String | 用户真实姓名（若实名）
idCard   | String | 身份证号码（若实名）

#### 请求示例(Request)
```
{
    "userName":"marlon",
    "password":"dkfhdklflkas15dfdjmfl"
}
```
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
	"data":null
}
```

### 获取条烟列表
#### 请求方式
`GET`
#### API
```
"smoke/lists"
```
#### 请求参数

名称（name） | 类型（Type）| 说明 
---|---|---
token | String | 用户鉴权标识
#### 返回参数
名称（name） | 类型（Type）| 说明 
---|---|---
id       | long   | 烟ID
smokeName| String | 烟名
smokeBarCode   | String | 烟条码
smokeCoding    | String | 烟编码
images   | Array | 烟图片Url
#### 请求示例(Request)
```
{
    "token":"jdfidjfsdkfeiepwers55df4"
}
```
#### 返回示例（Response）
`成功时：`
```
{
	"code": 200,
	"msg": "success",
	"data": [{
		"id": "1",
		"smokeName": "中南海(典5)",
		"smokeBarCode": "6901028010351",
		"smokeCoding": "1101016",
		"images": ["https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=1400792195,654294006&fm=26&gp=0.jpg", "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1548150135180&di=10d9eac73420e1eb2691025f4c65e49d&imgtype=0&src=http%3A%2F%2Fpic1.16pic.com%2F00%2F10%2F57%2F16pic_1057476_b.jpg", "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1548150206371&di=84044340ba4ae96b7f6cb6ee2295ff2b&imgtype=0&src=http%3A%2F%2Fpic13.997788.com%2F_pic_auction%2F00%2F01%2F65%2F48%2F1654810d.jpg"]
	}, {
		"id": "2",
		"smokeName": "钻石（一品荷花）",
		"smokeBarCode": "6901028250481",
		"smokeCoding": "1303022",
		"images": ["https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=1400792195,654294006&fm=26&gp=0.jpg", "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1548150135180&di=10d9eac73420e1eb2691025f4c65e49d&imgtype=0&src=http%3A%2F%2Fpic1.16pic.com%2F00%2F10%2F57%2F16pic_1057476_b.jpg", "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1548150206371&di=84044340ba4ae96b7f6cb6ee2295ff2b&imgtype=0&src=http%3A%2F%2Fpic13.997788.com%2F_pic_auction%2F00%2F01%2F65%2F48%2F1654810d.jpg"]

	}, {
		"id": "3",
		"smokeName": "钻石（西柏坡）",
		"smokeBarCode": "6901028079082",
		"smokeCoding": "1303023",
		"images": ["https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=1400792195,654294006&fm=26&gp=0.jpg", "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1548150135180&di=10d9eac73420e1eb2691025f4c65e49d&imgtype=0&src=http%3A%2F%2Fpic1.16pic.com%2F00%2F10%2F57%2F16pic_1057476_b.jpg", "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1548150206371&di=84044340ba4ae96b7f6cb6ee2295ff2b&imgtype=0&src=http%3A%2F%2Fpic13.997788.com%2F_pic_auction%2F00%2F01%2F65%2F48%2F1654810d.jpg"]
	}]
}
```
`失败时：`
```
{
    "code": 非200,
	"msg": "错误提示信息",
	"data":null
}
```
### 添加新烟
#### 请求方式
`POST`
#### API
```
"smoke/add"
```
#### 请求参数
名称（name） | 类型（Type）| 说明 
---|---|---
token | String | 用户鉴权标识
smokeName   | String | 烟名
smokeBarCode  | String | 烟条码
smokeCoding | String | 烟编码
images | File | 烟图片

#### 请求示例（Request）
```
{
    "token":"jdfidjfsdkfeiepwers55df4",
    "smokeName":"钻石(荷花绿水青山)",
    "smokeBarCode":"6901028079051",
    "smokeCoding":"1303024",
    "images":FILE
}
```
#### 返回示例（Response）
`成功时：`
```
{
    "code": 200,
    "msg": "success",
    "data": null
}
```
`失败时：`
```
{
    "code": 非200,
	"msg": "错误提示信息",
	"data":null
}
```
### 删除已有烟
#### 请求方式
`POST`
#### API
```
"smoke/delete"
```
#### 请求参数
名称（name） | 类型（Type）| 说明 
---|---|---
token | String | 用户鉴权标识
smokeBarCode  | String | 烟条码

#### 请求示例（Request）
```
{
    "token":"jdfidjfsdkfeiepwers55df4",
    "smokeBarCode":"6901028079082",
}
```
#### 返回示例（Response）
`成功时：`
```
{
    "code": 200,
    "msg": "success",
    "data": null
}
```
`失败时：`
```
{
    "code": 非200,
	"msg": "错误提示信息",
	"data":null
}
```

### 更新已有烟
#### 请求方式
`POST`
#### API
```
"smoke/update"
```
#### 请求参数
名称（name） | 类型（Type）| 说明 
---|---|---
token | String | 用户鉴权标识
smokeBarCode  | String | 烟条码
smokeName   | String | 烟名
smokeCoding | String | 烟编码
oldimages | Array | 要更改图片的url
images | File | 烟图片

#### 请求示例（Request）
```
{
    "token":"jdfidjfsdkfeiepwers55df4",
    "smokeBarCode":"6901028010351",
    "smokeName":"中南海(典5)",
    "smokeCoding":"1101016",
    "oldimages":["https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=1400792195,654294006&fm=26&gp=0.jpg", "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1548150135180&di=10d9eac73420e1eb2691025f4c65e49d&imgtype=0&src=http%3A%2F%2Fpic1.16pic.com%2F00%2F10%2F57%2F16pic_1057476_b.jpg"]
    "images":FILE
    
    
}
```
#### 返回示例（Response）
`成功时：`
```
{
    "code": 200,
    "msg": "success",
    "data": null
}
```
`失败时：`
```
{
    "code": 非200,
	"msg": "错误提示信息",
	"data":null
}
```
