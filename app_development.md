# 幻腾高级应用开发指南

## 主流程

1. 注册幻腾账号,注册应用
2. 接入幻腾Oauth认证,获取访问相应Api的权限.
3. 接入幻腾推送服务, 建立长连接监听消息推送.
4. 实现自己的服务逻辑,输入是Api获取的数据和推送设备状态,输出是通过Api控制设备.

## 数据流向示意图

![高级应用数据流向](https://github.com/HuanTeng/huanteng.github.io/blob/master/images/高级应用数据流向.png)

## 相关资料

* [幻腾OAuth认证接入指南](https://github.com/HuanTeng/huanteng.github.io/blob/master/oauth.md)
* [幻腾接口总则](https://github.com/HuanTeng/huanteng.github.io/blob/master/main.pdf)
* [幻腾推送服务接入说明](https://github.com/HuanTeng/huanteng.github.io/blob/master/notification.md)
* [Api文档和调试页面](http://huantengsmart.com/doc/api_v1)


## Q & A

```
Q: 接口总则太长了,重点是什么?
```

* A: 幻腾接口总则里面最重要的就是这段, 请求Api务必要给Accept报头.

	> 请使用“application/vnd.huantengsmart-版本号+json”作为Accept报头的内容。如果未传或传递了不正
确的Accept报头,服务器将返回HTTP/1.1 406 Not Acceptable. 示例. Accept: application/vnd.huantengsmart-v1+json
	>

```
Q: 我能用RFC2617基本身份认证或者RFC6749中定义的OAuth2这两种身份认证方式么?
```

* A: 如果你只想访问Api的话,是可以的,但推送服务就不行了.接口总则里面的旧认证方式会逐步废弃,建议不要使用.

```
Q:为什么我在Api调试界面上调试数组参数怎么都失败?
```

* A: 这个是Swagger的bug, 实际上接口是没有bug的.

```
Q:我通过Api试图打开一个灯,服务器都返回200了,但为什么灯还没有打开?
```

* A: 控制设备的指令先到服务器,然后服务器推给本地网关,再通过本地网络到达设备.这个过程是有延迟的. 服务器返回200只是说明服务器收到了,推送到达才算设备真正收到指令.

```
Q:我创建了应用要如何接收推送信息，推送信息的格式是什么样的?
```

* A: 我们会向你创建应用时填写的 Notificatin Url 发起 POST 请求 并携带有Json格式的推送信息示例如下

	```
	{
		"type": "DoorSensorsChanged-v2-1462353745",
		"content": {
			"door_sensor_id": 1126,
			"is_open": false,
			"alert_mode": 0,
			"alert_status": 1,
			"behaviors": [{
				"action": "close",
				"timestamp": 1462934721000
			}]
		}
	}
	```
	`content` 中的内容会根据不同的设备有略微的不同

```
Q:推送信息为什么会有延迟
```

* A: 当频繁操作设备时推送服务器可能会产生短暂的延迟，延迟过后会同时推送多条信息，此时需要注意的是需要将这些信息按照时间戳自行排序与设备操作相对应，不能按照收到的先后顺序作为对应设备操作的判断依据
