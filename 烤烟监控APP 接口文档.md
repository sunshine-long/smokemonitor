
# 测试环境
```
通信协议：http
IP：192.168.0.103（暂定）
Port：8089（暂定）
```
# 测试目的

测试烤烟过程中，相关数据推送，和紧急事件报警。
# APP相关功能和交互流程
### 常规交互流程
1.	登录APP，进入主页
2.	获取烤烟历史消息列表，
3.	点击列表中任意一项，查看交互流程
### 消息推送交互流程
1.	收到推送消息，
2.	点击消息，判断此时是否登录过期；
过期，跳转到登录页面，先登录，登录成功，跳转到消息详情页；
未过期，直接跳转到消息详情页。
# 相关约定:
```
BaseResponse{
	int code; 		//成功 200，失败 非200。
	String msg; 	//成功（返回success），失败（相关错误信息）。
	Object data;	//返回相关请求数据，这里的data，任意数据结构，没有时返回null。
}
```
# 相关类：

```
MessageBean {
    //消息ID
    private Integer messageID;
    //消息时间
    private String time;
    //当前烤烟温度
    private String temperature;
    //烤烟机编号
    private String tobaccoMachineNo;
    //当前烤烟湿度
    private String humidity;
    //消息的类型（普通消息/紧急报警消息）
    private String type;
}
```
```
MessageDetailBean {
//相关描述信息
    private String description;
    //对应的图片数据
    private List<String> images;
    //用于绘制温度湿度变化曲线
    private List<OvenStatus> ovenStatuses;
    //消息时间
    private String time;
}
```
```
OvenStatus {
    //时间
    private String time;
    //温度
    private String temperature;
    //湿度
    private String humidity;
}
```
```
Userinfo {
//没用的信息可以暂时不返回
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
    //个人描述
    private String description;
}
```
# 登录
### 描述：
用于用户登录，完成稿后并绑定推送ID，用于定向推送消息。
### API：
`"/user/login"`
### 请求方式：
`POST`
### Request：
```
{
	"username": "marlon",
	"password": "123456"   //这里可以rsa加密一下
}
```
### Response：
```
{
	"code": 200,
	"msg": "success",
	"data": {
		"username": "marlon",
		"passwords": "123456",
		"avatar": "null",
		"token": "string",
		"userID": 15456645585,
		"mobile": " null",
		"realName": "null",
		"description": "null"
	}
}
```
# 获取消息列表
### 描述：
获取历史消息列表信息
### API:
`"/message/lists"`
### 请求方式：
`GET`
### Request：
`null`
### Response：
```
{
	"code": 200,
	"msg": "success",
	"data": [{
		"time": "2018-10-24 10:38:44",
		"messageID": "121",
		"temperature": "60C°",
		"humidity": "30%",
		"tobaccoMachineNo": "NO 1",
		"type": "normal",
		"startTime": "2018-10-24 08:38:44",
		"endTime": "2018-10-24 10:38:44"
	}, {
		"time": "2018-10-24 10:36:44",
		"messageID": "122",
		"temperature": "60C°",
		"humidity": "30%",
		"tobaccoMachineNo": "NO 1",
		"type": "normal",
		"startTime": "2018-10-24 08:38:44",
		"endTime": "2018-10-24 10:38:44"
	}, {
		"time": "2018-10-24 10:50:44",
		"messageID": "123",
		"temperature": "60C°",
		"humidity": "30%",
		"tobaccoMachineNo": "NO 1",
		"type": "normal",
		"startTime": "2018-10-24 08:38:44",
		"endTime": "2018-10-24 10:38:44"
	}]
}
```
# 消息详情
### 描述：
用于获取消息详情信息
### API:
`"/message/lists/{messageID}"`
### 请求方式：
`GET`
### Request：
```
{
"messageID":"121"
}
```
### Response：
```
{
	"code": 200,
	"msg": "success",
	"data": {
		"messageID":"121",		
		"time": "2018-10-24 10:38:44",
		"description": "随便搞一批阿拉的文字啊，描述烟叶和烤箱的状态，就可以啦",
		"images": ["https://s.click.taobao.com/t?e=m=2&s=7WCg0+pzKwgcQipKwQzePCperVdZeJviK7Vc7tFgwiFRAdhuF14FMa2XsNgKZ+Oxt4hWD5k2kjP/TrTNBNETjAtOHPHN0vssKO4N//7xLcVZMTj583r1vqUuZxIcp9pfUIgVEmFmgnaR4ypTBJBwtC8UTyjdhQwHJPwiig1bxLMnyi1UQ/17I10hO9fBPG8oXH+QH9e66Y4=",
			"https://www.hao123.com/link/https/?key=http://www.baidu.com/?tn=sitehao123&&monkey=m-search-baidulogo&c=B7E43E11C0EFBBCC1D5F11E3A6A11135",
			"https://www.hao123.com/link/https/?key=http://www.baidu.com/?tn=sitehao123&&monkey=m-search-baidulogo&c=B7E43E11C0EFBBCC1D5F11E3A6A11135",
			"http://www.hao123.com/redian/sheshouyef.htm"
		],
		"ovenStatuses": [{
			"time": "2018-10-24 10:38:44",
			"temperature": "60C°",
			"humidity": "30%"
		}, {
			"time": "2018-10-24 10:36:44",
			"temperature": "60C°",
			"humidity": "30%"
		}, {
			"time": "2018-10-24 10:50:44",
			"temperature": "60C°",
			"humidity": "30%"
		}]
	}
}
```
