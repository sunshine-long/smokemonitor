
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
# 接口
### 获取条烟列表
### API
```
"smoke/lists"
```
### 请求方式
`GET`
### Request
`null`
### Response
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
### 添加新烟
### API
```
"smoke/add"
```
### 参数
```
name               type                 说明
smokeName          String	        烟名
smokeBarCode       String	        烟条码
smokeCoding        String               烟编码
images             file                 烟图片                  
```
### 请求方式
`POST`
### Request
```
{
"smokeName":"新烟",
"smokeBarCode":"",
"smokeCoding":"",
"images":FILE,
}
```
### Response
```
{
"code": 200,
"msg": "success",
"data": null
```
