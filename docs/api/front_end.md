## copyText

描述：复制文本

参数：

+ `content`：要复制的纯文本 [`String`]（必填）

示例
```js
this.$copyText("xuanzai")
```

## File

###  getImgFile

描述：获取图片信息，图片预览

参数：

+ `limit`：文件大小 [`Number`] 单位：兆（选填：默认限制文件大小为2M）

返回值：`Promise`

+ `raw`：二进制文件
+ `url`: base64

示例：
```js
this
	.$getImgFile(limit)
	.then((raw, url) => {
		// todo
	})
```

## Date

日期格式化方法。

### formatDate

描述：将日期格式化为`yyyy-MM-dd HH:mm:ss`

参数：

+ `date`: 日期对象[`Date`]（必填）
+ `isAccurate`: 是否精确到时分秒[`Boolean`]（选填：默认为`false`）

返回值：`String`

示例：
```js
this.$formatDate(new Date()) // 2019-11-05
this.$formatDate(new Date(), true) // 2019-11-05 10:06:31
```

### dateDiff

描述：两个日期的时间差

参数：

+ `sDate1`: 结束日期[`Date`]（必填）
+ `sDate2`: 开始日期[`Date`]（必填）
+ `isNegative`: 只能是结束日期减开始日期，返回的值可能为负值（选填：默认为`false`）

返回值：`Object`

示例：
```js
this.$dateDiff(new Date('2019-11-05'), new Date('2019-11-01'))
// { 时间戳 stamp: xxx, 相差总秒数 seconds:xxx, 相差总分钟数 minutes: xxx, 相差总小时数 hours: xxx, 相差总天数 days: xxx, 相差总星期数 weeks: xxx, 时分秒 times: xxx}
```

### setDay

描述：设置日期

参数：

+ `date`: 日期[`Date`]（必填）
+ `number`: 天数[`Number`]（选填，默认为0）
+ `isAccurate`: 是否精确到时分秒[`Boolean`]（选填，默认为`false`）

返回值：`String`

示例：
```js
this.$setDay(new Date(), 3, true) // 返回后三天 YYYY-MM-DD HH:mm:ss
this.$setDay(new Date(), -3, false) // 返回前三天 YYYY-MM-DD
```

### setMonth

描述：设置月份

参数：

+ `date`: 日期[`Date`]（必填）
+ `number`: 天数[`Number`]（选填，默认为0）
+ `isAccurate`: 是否精确到时分秒[`Boolean`]（选填，默认为`false`）

返回值：`String`

示例：
```js
this.$setMonth(new Date(), 3, true) // 返回后三个月 YYYY-MM-DD HH:mm:ss
this.$setMonth(new Date(), -3, false) // 返回前三个月 YYYY-MM-DD
```

### setYear

描述：设置年份

参数：

+ `date`: 日期[`Date`]（必填）
+ `number`: 天数[`Number`]（选填，默认为0）
+ `isAccurate`: 是否精确到时分秒[`Boolean`]（选填，默认为`false`）

返回值：`String`

示例：
```js
this.$setYear(new Date(), 3, true) // 返回后三年 YYYY-MM-DD HH:mm:ss
this.$setYear(new Date(), -3, false) // 返回前三年 YYYY-MM-DD
```

### setDate

描述：获取前n天

参数：

+ `date`: 日期[`Date`]（必填）
+ `options`: 天数[`Object`]（选填，默认为0）
	+ `years`: 年份[`Number`]（选填，默认为0）
	+ `quarters`: 季度[`quarters`]（选填，默认为0）
	+ `months`: 月份[`Number`]（选填，默认为0）
	+ `weeks`: 周[`Number`]（选填，默认为0）
	+ `days`: 天[`Number`]（选填，默认为0）
	+ `hours`: 小时[`Number`]（选填，默认为0）
	+ `minutes`: 分钟[`Number`]（选填，默认为0）
	+ `seconds`: 秒[`Number`]（选填，默认为0）
	+ `milliseconds`: 毫秒[`Number`]（选填，默认为0）
+ `rules`: 时间规则[`String`]（选填，默认为`YYYY-MM-DD HH:mm:ss`）

返回值：`Object`

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

+ `date`: 相对于现在的日期[`Date`]（默认为当前时间）

返回值：`String`

示例：
```js
this.$fromNow(new Date()) // 几秒前
```

## storage

通过`localStorage`进行简单的封装。

### setMemoryPmt

描述：长久存储，写入

参数：

+ `key`: 键 [`String`]（必填）
+ `value`: 值 [`Any`]（必填）
  
示例：
```js
this.$setMemoryPmt("name", "xuanzai")
```

### getMemoryPmt

描述：长久存储，读取

参数：

+ `key`: 键 [`String`]（必填）

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

+ `url`：路由地址[`String`]（必填）

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

+ `delta`：返回的页面数，如果`delta`大于现有页面数，则返回到首页

示例：
```js
this.$navigateBack() // 默认返回一页
this.$navigateBack(3) // 返回到前三页，如果页面数大于页面栈数，返回到首页
```

### switchTab

描述：返回到`tab`页面，页面栈清空

参数：

+ `url`：路由地址[`String`]（必填）
+ `success`：成功回调
+ `fail`：失败回调
+ `complete`: 完成回调

示例：
```js
this.$switchTab({ url: "/pages/home/index" })
```

### redirectTo

描述：关闭当前页面，跳转到相应路由页面

参数：

+ `url`：路由地址[`String`]（必填）

示例：
```js
this.$redirectTo({ url: "/pages/home/index" })
```

### reLaunch

描述：关闭所有页面，跳转到相应页面，此时页面栈数为2

参数：

+ `url`：路由地址[`String`]（必填）
+ `success`：成功回调
+ `fail`：失败回调
+ `complete`: 完成回调

示例：
```js
this.$reLaunch({ url: "/pages/home/index" })
```

## Message

通过`uniapp`的提示信息进行二次封装。

### showToast

描述：冒泡提示

参数：

+ `title`: 提示语 [`String`]（选填，默认为空）
+ `icon`: 提示图标[`String`]（选填，默认为`success`）
+ `mask`: 是否有遮罩[`Boolean`]（选填，默认为`false`）
+ `duration`: 持续时长[`Number`]（选填，默认为1.5秒）
+ `success`：成功回调
+ `fail`：失败回调
+ `complete`: 完成回调

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

+ `title`: 提示语 [`String`]（选填，默认为空）
+ `mask`: 是否有遮罩[`Boolean`]（选填，默认为`false`）
+ `success`：成功回调
+ `fail`：失败回调
+ `complete`: 完成回调

示例：
```js
this.$showLoading()
```

### showModal

描述：弹窗提示

参数：

+ `title`: 标题 [`String`]（选填，默认为空）
+ `content`: 内容 [`String`]（选填，默认为空）
+ `mask`: 是否有遮罩[`Boolean`]（选填，默认为`false`）
+ `showCancel`: 是否显示取消按钮[`Boolean`]（选填，默认为`false`）
+ `cancelText`: 取消按钮文本内容[`String`]（选填，默认为取消）
+ `confirmText`: 确认文本文字[`String`]（选填，默认为确认）
+ `cancelColor`: 取消按钮颜色[`String`]（选填，默认颜色因各端而不同）
+ `confirmColor`: 确认按钮颜色[`String`]（选填，默认颜色因各端而不同）
+ `success`：成功回调
	+ 返回值：e
		+ `confirm`: 点击确认时返回`true`，否则返回`false`
+ `fail`：失败回调
+ `complete`: 完成回调

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

## wxLogin

描述：`H5`微信登录

> 注意：仅在编译为`H5`时生效

返回值：`code`

示例：
```js
this.$wxLogin() // code
```

## wxPay

描述：`H5`微信支付

> 注意：仅在编译为`H5`时生效

参数：

+ `options`：微信支付参数[`Object`]（必填）
	+ `debug`：是否开启调试模式[`Boolean`]（选填，默认为`false`）
	+ `timestamp`：生成签名的时间戳[`String`]（必填）
	+ `nonceStr`：生成签名随机字符串[`String`]（必填）
	+ `signature`：生成签名[`String`]（必填）
	+ `packageValue`：统一支付接口返回的prepay_id参数值[`String`]（必填）
	+ `paySign`：支付签名[`String`]（必填）
+ `success`：成功回调
+ `fali`：失败回调
+ `complete`：完成回调

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

> 注意：仅在编译为`H5`时生效

参数：

+ `options`：微信支付参数[`Object`]（必填）
	+ `debug`：是否开启调试模式[`Boolean`]（选填，默认为`false`）
	+ `timestamp`：生成签名的时间戳[`String`]（必填）
	+ `nonceStr`：生成签名随机字符串[`String`]（必填）
	+ `signature`：生成签名[`String`]（必填）
	+ `title`：分享标题[`String`]（必填）
	+ `desc`：分享内容描述[`String`]（必填）
	+ `link`：分享链接[`String`]（必填）
	+ `imgUrl`：分享图片[`String`]（必填）
+ `success`：成功回调
+ `fali`：失败回调
+ `complete`：完成回调

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

> 注意：仅在编译为微信小程序时生效，调用时需要配合

返回值：`Promise`

+ `userLocation`: 允许获取用户定位信息[`Boolean`]，不允许则为`false`
+ `locationBackground`: 允许用户在将小程序置为后台时持续定位[`Boolean`]，不允许则为`false`

示例：
```js
this
	.$getLocationAuth()
	.then(result => {
		//result { userLocation: false, locationBackground: false }
	})
```