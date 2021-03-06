## copyText

描述：复制文本

传参：

参数 | 类型 | 必填 | 说明
- | - | - | -
content | String | 是 | 复制的纯文本

示例
```js
this
	.$copyText("xuanzai")
	.then(result => {
		// success to do
	})
```

## File

###  getFile

描述：获取文件

> 注意：仅在编译为h5时生效

传参：

参数 | 类型 | 必填 | 说明
- | - | - | -
limit | Number | 否 | 限制文件的总大小，单位：`兆`，默认文件总大小为`10M`
count | Number | 否 | 限制文件选择数量，默认最多一次性选择3个文件

返回值：`Promise`

参数 | 类型 | 说明
- | - | -
fileList | Array | 返回文件数组。当选择的文件不满足上述传参条件或默认参数条件，则会被`catch`捕捉

示例：
```js
this
	.$getImgFile(20, 10) // 限制上传文件总数量为20M，数量为10个
	.then(result => { // [file_1, file_2, ...]
		// todo
	})
```

###  getImgFile

描述：获取图片信息，图片预览

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
limit | Number | 否 | 限制图片的总大小，单位：`兆`，默认图片总大小为`10M`
count | Number | 否 | 限制图片的选择数量，默认最多一次性选择3个文件

返回值：`Promise`

参数 | 类型 | 说明
- | - | -
fileList | Array | 返回元素为对象的数组，见示例。当选择的文件不满足上述传参条件或默认参数条件，则会被`catch`捕捉

示例：
```js
this
	.$getImgFile(20, 10) // 限制上传图片总数量为20M，数量为10张
	.then(result => { // [{raw: File, url: base64}, ...]
		// todo
	})
```

### rotateImage

描述：将翻转的图片摆正，一般搭配`uni.chooseImage`使用

> 注意：仅在编译为非h5平台生效

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
img | String | 是 | 图片地址
cb | Function | 否 | 回调方法，方法接收的参数为图片的`url`

示例：
```js
this.$rotateImage(img, url => {
	// todo
})
```

### compressImageFile

描述：压缩图片文件

> 注意：仅在编译为h5平台生效

`options`参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
file | file | 是 | 文件
quality | Number | 否 | 文件质量，默认质量为`0.7`

返回值：`Promise`

参数 | 类型 | 说明
- | - | -
raw | File | 文件对象

示例：
```js
this
	.$compressFile(
		file,
		quality
	)
	.then(raw => {
		// todo
	})
```

### download

描述：下载文件

`options`中的参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
url | String | 是 | 文件地址
fileName | Function | 否 | 文件名称，`h5`中部分浏览器如`chrome`与`fireFox`生效，其他端无效
isLoading | Boolean | 否 | 是否显示加载更多，默认值为`false`

返回值：`downloadTask`

该对象一般用于监听下载进度，[具体用法参考uniapp-downloadFile](https://uniapp.dcloud.io/api/request/network-file?id=downloadfile)

示例：
```js
this.$download({
	url: "https://myinterface.xuanzai.top/getPicture" // 文件地址,
	fileName: 'image',
	isLoading: true
})
```

### dataUrlToBlob

描述：将`base64`数据转为`blob`

> 注意：仅在编译为H5时生效

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
dataurl | String | 是 | base64

示例：
```js
this.$dataUrlToBlob(base64) // blob
```


## Date

日期格式化方法。

### formatDate

描述：将日期格式化为`yyyy-MM-dd HH:mm:ss`

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
date | Date | 是 | 接收的日期对象
isAccurate | Boolean | 否 | 是否精确到时分秒，默认值为`false`

返回值：

参数 | 类型 | 说明
- | - | -
date | String | 常用的日期字符串，具体见示例

示例：
```js
this.$formatDate(new Date()) // 2019-11-05
this.$formatDate(new Date(), true) // 2019-11-05 10:06:31
```

### dateDiff

描述：两个日期的时间差

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
sDate1 | Date | 是 | 接收的日期对象
sDate2 | Date | 是 | 是否精确到时分秒，默认值为`false`

返回值：`Object`

参数 | 类型 | 说明
- | - | -
stamp | Number | 时间戳差值
seconds | Number | 相差总秒数，向下取整
minutes | Number | 相差总分钟数，向下取整
hours | Number | 相差总小时数，向下取整
days | Number | 相差总天数，向下取整
weeks | Number | 相差总星期数，向下取整
times | String | 相差标准时分秒：hh:mm:ss

示例：
```js
this.$dateDiff(new Date('2019-11-05'), new Date('2019-11-01'))
// { 时间戳 stamp: xxx, 相差总秒数 seconds:xxx, 相差总分钟数 minutes: xxx, 相差总小时数 hours: xxx, 相差总天数 days: xxx, 相差总星期数 weeks: xxx, 时分秒 times: xxx}
```

### setDay

描述：设置日期

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
date | Date | 是 | 接收的日期对象
number | Number | 是 | 设置的天数，负数则往前计算
isAccurate | Boolean | 否 | 是否精确到时分秒，默认值为`false`

返回值：

参数 | 类型 | 说明
- | - | -
date | String | 常用的日期字符串，具体见示例

示例：
```js
this.$setDay(new Date(), 3, true) // 返回后三天 YYYY-MM-DD HH:mm:ss
this.$setDay(new Date(), -3, false) // 返回前三天 YYYY-MM-DD
```

### setMonth

描述：设置月份

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
date | Date | 是 | 接收的日期对象
number | Number | 是 | 设置的月数，负数则往前计算
isAccurate | Boolean | 否 | 是否精确到时分秒，默认值为`false`

返回值：

参数 | 类型 | 说明
- | - | -
date | String | 常用的日期字符串，具体见示例

示例：
```js
this.$setMonth(new Date(), 3, true) // 返回后三个月 YYYY-MM-DD HH:mm:ss
this.$setMonth(new Date(), -3, false) // 返回前三个月 YYYY-MM-DD
```

### setYear

描述：设置年份

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
date | Date | 是 | 接收的日期对象
number | Number | 是 | 设置的年数，负数则往前计算
isAccurate | Boolean | 否 | 是否精确到时分秒，默认值为`false`

返回值：

参数 | 类型 | 说明
- | - | -
date | String | 常用的日期字符串，具体见示例

示例：
```js
this.$setYear(new Date(), 3, true) // 返回后三年 YYYY-MM-DD HH:mm:ss
this.$setYear(new Date(), -3, false) // 返回前三年 YYYY-MM-DD
```

### setDate

描述：获取前n天

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
date | Date | 是 | 接收的日期对象
options | Object | 是 | 日期设置配置对象
rules | String | 否 | 日期格式，默认为`YYYY-MM-DD HH:mm:ss`

`options`参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
years | Number | 否 | 设置年份，负数则往前计算
quarters | Number | 否 | 设置季度（三个月一季度），负数则往前计算
months | Number | 否 | 设置月份，负数则往前计算
weeks | Number | 否 | 设置星期，负数则往前计算
days | Number | 否 | 设置天数，负数则往前计算
hours | Number | 否 | 设置小时，负数则往前计算
minutes | Number | 否 | 设置分钟数，负数则往前计算
seconds | Number | 否 | 设置秒数，负数则往前计算
milliseconds | Number | 否 | 设置毫秒数，负数则往前计算

返回值：

参数 | 类型 | 说明
- | - | -
date | String | 常用的日期字符串，具体见示例

示例：
```js
this.$setDate(new Date(), {
	years: 1
}) // 当前时间往后加一年 YYYY-MM-DD HH:mm:ss
this.$setDate(new Date(), {
	months: -1,
	hours: 1
}, 'YYYY-MM') // 当前时间减一个月并加一个小时 YYYY-MM
```

### fromNow

描述：获取相对时间

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
date | Date | 否 | 相对于现在的日期，默认为当前时间

返回值：

参数 | 类型 | 说明
- | - | -
date | String | 常用的日期字符串，具体见示例

示例：
```js
this.$fromNow(new Date()) // 几秒前
```

## Location

> 注意：仅在编译为非`H5`平台时生效，编译为小程序需要在服务器域名中添加合法域名https://apis.map.qq.com

### getLocation

描述：获取当前/指定位置的经纬度

参数 | 类型 | 必填 | 说明
- | - | - | -
address | String | 否 | 地址信息

返回值：经纬度对象

示例：
```js
// 获取当前位置经纬度
this
	.$getLocation()
	.then(res => {
		// res: { latitude, longitude }
	})
	
// 获取指定位置经纬度
this
	.$getLocation('广东省广州市天河区体育西路')
	.then(res => {
		// res: { latitude, longitude }
	})
```

### getAddress

描述：获取当前位置信息

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
latitude | Number/String | 是 | 纬度
longitude | Number/String | 是 | 经度

返回值：地址信息对象

示例
```js
this
	.$getAddress(lat, lng)
	.then(res => {
		// res: 地址详情
	})
	
// 结合getLocation获取当前位置信息
this
	.$getLocation()
	.then(res => {
		this
			.$getAddress(res.latitude, res.longitude)
			.then(res => {
				// todo
			})
	})
```

## storage

通过`localStorage`进行简单的封装。

### setMemoryPmt

描述：长久存储，写入，用法与`localStorage.setItem`相似，无需对值进行处理

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
key | String | 是 | 键
value | String | 是 | 值

示例：
```js
this.$setMemoryPmt("name", "xuanzai")
```

### getMemoryPmt

描述：长久存储，读取，用法与`localStorage.getItem`相似，无需对值进行处理

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
key | String | 是 | 键

返回值：根据`this.$setMemoryPmt`的值决定

示例：
```js
this.$getMemoryPmt("name")
```

## Navigate

导航到对应页面

### navigateTo

描述：跳转到对应页面，页面栈增加

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
url | String | 是 | 路由地址

示例：
```js
this.$navigateTo({ url: "/pages/home/index" })
```

带参数示例：
```js
// 页面A
this.$navigateTo({ url: "/pages/home/index?id=1" })

// 页面B
onLoad(query) {
	console.log(query.id) // 1
}
```

### navigateBack

描述：页面返回，页面栈减少

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
delta | Number | 否 | 返回的页面数，如果`delta`大于现有页面数，则返回到首页


示例：
```js
this.$navigateBack() // 默认返回一页
this.$navigateBack(3) // 返回到前三页，如果页面数大于页面栈数，返回到首页
```

### switchTab

描述：返回到`tab`页面，页面栈清空

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
url | String | 是 | 路由地址

示例：
```js
this.$switchTab({ url: "/pages/home/index" })
```

### redirectTo

描述：关闭当前页面，跳转到相应路由页面

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
url | String | 是 | 路由地址

示例：
```js
this.$redirectTo({ url: "/pages/home/index" })
```

### reLaunch

描述：关闭所有页面，跳转到相应页面，此时页面栈数为2

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
url | String | 是 | 路由地址

示例：
```js
this.$reLaunch({ url: "/pages/home/index" })
```

## Message

通过`uniapp`的提示信息进行二次封装。

### showToast

描述：冒泡提示

参数：

[具体参考uniapp-showToast](https://uniapp.dcloud.io/api/ui/prompt?id=showtoast)

示例：
```js
this.$showToast({
	icon: "success",
	title: "成功"
})
```

### showLoading

描述：加载提示

参数：

[具体参考uniapp-showLoading](https://uniapp.dcloud.io/api/ui/prompt?id=showloading)

示例：
```js
this.$showLoading()
```

### showModal

描述：弹窗提示

参数：

[具体参考uniapp-showModal](https://uniapp.dcloud.io/api/ui/prompt?id=showmodal)

示例：
```js
this.$showModal({
	content: "内容",
	success: e => {
		if(e.confirm) {
			console.log("点击确认")
		} else {
			console.log("点击取消")
		}
	}
})
```

## Bluetooth

通过`uniapp`的蓝牙模块进行二次封装。

### openBluetoothAdapter

描述：打开蓝牙适配器，在连接蓝牙设备之前必须先进行这一步操作

示例：
```js
this
	.$openBluetoothAdapter()
	.then(result => {
		// todo
	})
	.catch(e => {
		this.$showModal({
			title: "蓝牙初始化失败",
			content: "请打开你的手机蓝牙以便连接设备",
			success: e => {
				if(e.confirm) {
					// todo
				}
			}
		})
	})
```

### startBluetoothDeviceDiscovery

描述：通过蓝牙设备名称查找对应的蓝牙设备

> tips: 由于`ios`设备获取到的蓝牙设备`deviceId`不一致，所以需要通过蓝牙设备名称去获取设备的`deviceId`以便连接设备

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
name | String | 是 | 设备名称

`Promise`返回值：

参数 | 类型 | 说明
- | - | - | -
result | String | 设备ID

示例：
```js
// 用法
this
	.$startBluetoothDevicesDiscovery(name)
	.then(result => {
		// todo
	})
	.catch(e => {
		this.$showToast({
			icon: "none",
			title: "没有找到相应设备"
		})
	})

// 具体使用场景，先初始化蓝牙 ---> 再连接设备
this
	.$openBluetoothAdapter()
	.then(result => {
		this
			.$connectBle(deviceId)
			.then(result => {
				
			})
			.catch(e => {
				this.$showToast({
					icon: "none",
					title: "设备连接失败，请稍后再试"
				})
			})
	})
	.catch(e => {
		this.$showModal({
			title: "蓝牙初始化失败",
			content: "请打开你的手机蓝牙以便连接设备",
			success: e => {
				if(e.confirm) {
					// todo
				}
			}
		})
	})
```

### connectBle

描述：连接蓝牙设备

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
deviceId | String | 是 | 设备ID

示例：
```js
// 用法
this
	.$connectBle(deviceId)
	.then(result => {
		// todo
	})
	.catch(e => {
		this.$showToast({
			icon: "none",
			title: "设备连接失败，请稍后再试"
		})
	})

// 具体使用场景，先初始化蓝牙 ---> 再连接设备
this
	.$openBluetoothAdapter()
	.then(result => {
		this
			.$connectBle(deviceId)
			.then(result => {
				
			})
			.catch(e => {
				this.$showToast({
					icon: "none",
					title: "设备连接失败，请稍后再试"
				})
			})
	})
	.catch(e => {
		this.$showModal({
			title: "蓝牙初始化失败",
			content: "请打开你的手机蓝牙以便连接设备",
			success: e => {
				if(e.confirm) {
					// todo
				}
			}
		})
	})
```

### getBluetoothServices

描述：获取蓝牙服务列表

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
deviceId | String | 是 | 设备ID

`Promise`返回值：

参数 | 类型 | 说明
- | - | - | -
list | Array | 服务信息列表

示例：
```js
// 用法
this
	.$getBluetoothServices(deviceId)
	.then(result => {
		// todo
	})
	.catch(e => {
		this.$showToast({
			icon: "none",
			title: "获取设备服务列表错误"
		})
	})

// 具体使用场景，先初始化蓝牙 ---> 连接设备 ---> 获取服务列表 
this
	.$openBluetoothAdapter()
	.then(result => {
		this
			.$connectBle(deviceId)
			.then(result => {
				this
					.$getBluetoothServices(deviceId)
					.then(result => {
						// todo
					})
					.catch(e => {
						this.$showToast({
							icon: "none",
							title: "获取设备服务列表错误"
						})
					})
			})
			.catch(e => {
				this.$showToast({
					icon: "none",
					title: "设备连接失败，请稍后再试"
				})
			})
	})
	.catch(e => {
		this.$showModal({
			title: "蓝牙初始化失败",
			content: "请打开你的手机蓝牙以便连接设备",
			success: e => {
				if(e.confirm) {
					// todo
				}
			}
		})
	})
```

### getBluetoothCharacteristics

描述：获取蓝牙服务特征信息

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
deviceId | String | 是 | 设备ID
serviceId | String | 是 | 设备服务ID

`Promise`返回值：

参数 | 类型 | 说明
- | - | - | -
list | Array | 特征信息列表

示例：
```js
// 用法
this
	.$getBluetoothCharacteristics(deviceId, serviceId)
	.then(result => {
		// todo
	})
	.catch(e => {
		this.$showToast({
			icon: "none",
			title: "获取特征信息列表失败"
		})
	})

// 具体使用场景，先初始化蓝牙 ---> 连接设备 ---> 获取服务列表 ---> 获取特征列表
this
	.$openBluetoothAdapter()
	.then(result => {
		this
			.$connectBle(deviceId)
			.then(result => {
				this
					.$getBluetoothServices(deviceId)
					.then(result => {
						this
							.$getBluetoothCharacteristics(deviceId, serviceId)
							.then(result => {
								// todo
							})
					})
					.catch(e => {
						this.$showToast({
							icon: "none",
							title: "获取设备服务列表错误"
						})
					})
			})
			.catch(e => {
				this.$showToast({
					icon: "none",
					title: "设备连接失败，请稍后再试"
				})
			})
	})
	.catch(e => {
		this.$showModal({
			title: "蓝牙初始化失败",
			content: "请打开你的手机蓝牙以便连接设备",
			success: e => {
				if(e.confirm) {
					// todo
				}
			}
		})
	})
```

### sendServiceMsg

描述：向蓝牙设备发送信息

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
deviceId | String | 是 | 设备ID
serviceId | String | 是 | 设备服务uuid
characteristicId | String | 是 | 设备特征uuid
buffer | ArrayBuffer | 是 | 需要发送的信息

示例：
```js
// 用法
this
	.$sendServiceMsg(deviceId, serviceId, characteristicId, buffer)
	.then(result => {
		// todo
	})
	.catch(e => {
		this.$showToast({
			icon: "none",
			title: "发送信息失败"
		})
	})
```

### getServiceMsg

描述：获取蓝牙设备信息

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
deviceId | String | 是 | 设备ID
serviceId | String | 是 | 设备服务uuid
characteristicId | String | 是 | 设备特征uuid

示例：
```js
// 用法
this
	.$sendServiceMsg(deviceId, serviceId, characteristicId)
	.then(result => {
		// todo
	})
	.catch(e => {
		this.$showToast({
			icon: "none",
			title: "发送信息失败"
		})
	})
```

### stopService

描述：断开蓝牙设备

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
deviceId | String | 是 | 设备ID

示例：
```js
// 用法
this
	.$stopService(deviceId)
	.then(result => {
		// todo
	})
	.catch(e => {
		this.$showToast({
			icon: "none",
			title: "断开设备成功"
		})
	})
```

## http

通过`axios`进行二次封装，如需更多个性化，请前往`src/api/http/http.js`文件内进行更改

### http_normal

描述：`application/x-www-form-urlencoded`键值对的上传方式

参数详情参考[axios文档](https://www.kancloud.cn/yunye/axios/234845)

返回值：`Promise`

示例：
```js
this.$http_normal({
	url: "/xxx/xxx",
	method: "get",
	params: {
		name: "",
		age: ""
	}
}).then(result => {
	// todo
})

this.$http_normal({
	url: "/xxx/xxx",
	method: "post",
	data: {
		name: "",
		age: ""
	}
}).then(result => {
	// todo
})
```

### http_json

描述：`application/json`，`JSON`字符串的上传方式

参数详情参考[axios文档](https://www.kancloud.cn/yunye/axios/234845)

返回值：`Promise`

示例：
```js
this.$http_json({
	url: "/xxx/xxx",
	method: "get",
	params: {
		name: "",
		age: ""
	}
}).then(result => {
	// todo
})

this.$http_json({
	url: "/xxx/xxx",
	method: "post",
	data: {
		name: "",
		age: ""
	}
}).then(result => {
	// todo
})
```

### http_file

描述：`multipart/form-data`，多文件键值对的上传方式

参数详情参考[axios文档](https://www.kancloud.cn/yunye/axios/234845)

返回值：`Promise` 

`H5`示例：
```js
this.$http_file({
	url: "/xxx/xxx",
	method: "post",
	data: {
		name: "",
		age: ""，
		file_1: raw_1,
		file_2: raw_2
	}
}).then(result => {
	// todo
})
```

`小程序`示例：
```js
// 小程序只能上传一份文件，该文件数据存放在file字段里
this.$http_file({
	url: "/xxx/xxx",
	method: "post",
	data: {
		file: raw,
		name: "",
		age: ""
	}
}).then(result => {
	// todo
})
```

## App

封装`App`常用的一些方法

> tips：仅在`App`环境下使用，如要编译多端，请使用条件编译语句

### appUpdate

描述：检查`App`版本并弹窗更新

> 使用前请先让后台配置相应参数，参数如下

后台返回参数：

参数 | 类型 | 是否需要返回 |说明
- | - | - | -
version_code | String | 是 | 版本号
version_name | String | 是 | 版本名称
version_info | String | 是 | 版本信息 \n 换行（例如：1.修改了bug1 \n 2.修改了bug2 \n 3.修改了bug3）
forceUpdate | Boolean | 是 | 是否强制更新
downloadUrl | String | 是 | 版本下载链接 `IOS安装包更新请放跳转store应用商店链接,安卓apk放文件下载链接`

示例：
```js
this.$appUpdate()
```

### getCurrentNo

描述：获取当前`App`版本

参数：

参数 | 类型 | 是否必传 |说明
- | - | - | -
callback | Function | 是 | 返回`App`版本号

示例：
```js
this.$getCurrentNo(res => {
	// todo
})
```


## wxLogin

描述：`H5`微信登录

> 注意：仅在编译为`H5`时生效

返回值：`code`

参数：

参数 | 类型 | 说明
- | - | -
code | String | 回调地址后的那一串`code`值

示例：
```js
this.$wxLogin() // code
```

## jumpToOfficial

描述：`H5`跳转到对应公众号

> 注意：仅在编译为`H5`时生效

> 关于如何拿到base值？<br/>
> 1、登录公众号后台 <br/>
> 2、在公众号首页右键查看源码 <br/>
> 3、找到`commonData`参数，然后找到该对象里面的`uin_base64`值，并将该值传入函数即可

参数：

参数 | 类型 | 说明
- | - | -
uin_base64 | String | 公众号的base值

示例：
```js
this.$jumpToOfficial(uin_base64) 
```

## wxPay

描述：`H5`微信支付

> 注意：仅在编译为`H5`时生效

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
options | Object | 是 | 微信支付相关配置项
success | Function | 否 | 成功回调
fail | Function | 否 | 失败回调，接收错误参数
complete | Function | 否 | 完成回调

`options`的参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
timestamp | String | 是 | 生成签名的时间戳
nonceStr | String | 是 | 生成签名随机字符串
signature | String | 是 | 生成签名
packageValue | String | 是 | 统一支付接口返回的prepay_id参数值
paySign | String | 是 | 支付签名

> `options`中的签名相关参数通过后台请求获得

示例：
```js
this.$wxPay({
	timestamp,
	signature,
	nonceStr,
	packageValue,
	paySign
}, e => {
	console.log("支付成功")
}, e => {
	console.log("支付失败")
}, e => {
	console.log("调用接口结束")
})
```

## wxShare

描述：`H5`微信分享

> 注意：仅在编译为`H5`时生效，分享前先调用此接口，建议在onLoad、created等初始化生命周期内调用。

参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
options | Object | 是 | 微信分享相关配置项
success | Function | 否 | 成功回调
fail | Function | 否 | 失败回调，接收错误参数
complete | Function | 否 | 完成回调

`options`的参数：

参数 | 类型 | 必填 | 说明
- | - | - | -
timestamp | String | 是 | 生成签名的时间戳
nonceStr | String | 是 | 生成签名随机字符串
signature | String | 是 | 生成签名
title | String | 是 | 分享标题
desc | String | 是 | 分享内容描述
link | String | 是 | 分享链接
imgUrl | String | 是 | 分享图片

> `options`中的签名相关参数通过后台请求获得

示例：
```js
this.$wxShare({
	timestamp,
	signature,
	nonceStr,
	title,
	desc,
	link,
	imgUrl
}, e => {
	console.log("设置成功")
}, e => {
	console.log("设置失败")
}, e => {
	console.log("调用接口结束")
})
```

## getLocationAuth

描述：获取微信地理位置授权

> 注意：仅在编译为微信小程序时生效，调用时需要配合uni.openSetting使用

返回值：`Promise`

参数 | 类型 | 说明
- | - | -
userLocation | Boolean | 允许获取用户定位信息，不授权则返回`false`
locationBackground | Boolean | 允许用户在将小程序置为后台时持续定位，不授权则返回`false`

示例：
```js
this
	.$getLocationAuth()
	.then(result => { //result { userLocation: false, locationBackground: false }
		if(!result.userLocation || !result.locationBackground) {
			this.$showModal({
				content: "系统检测您为开启位置权限",
				success: e => {
					if(e.confirm) {
						uni.openSetting()
					}
				}
			})
		}
	})
```