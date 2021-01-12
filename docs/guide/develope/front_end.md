# 前端手册

## 文档

> [点击查看uniapp文档](https://uniapp.dcloud.io/)

<br/>

## 全局配置

在`global/js/config.js`文件下，有全局统一配置信息。操作这些信息方便改后打包使用。

这些属性时暂时的，往后会推出更多可配置项~

```js
// 布尔类型的值改为false则表示不允许设置
export default {
	// 是否默认H5微信登录
	isH5WxLogin: false,
	// 是否打开H5调试模式
	isDebug: true,
	// #ifdef APP-PLUS
	// App更新弹窗配置
	appUpdate: {
		// 主颜色
		mainColor: '#077ff9',
		// 弹窗图片url
		iconUrl: require('@/static/update.png'),
		// 是否点击遮罩关闭
		dialogClose: false,
		// 点击关闭后再次提醒时间(天)
		closeDay: 7,
		// 后台请求接口获取版本号
		requestUrl: '/api/user/get/version',
		// 是否进入App就检查并弹窗更新
		isUpdateImmediate: true
	}
	// #endif
}
```

<br/>

## 修改请求地址

请求地址在`global/js/baseUrl.js` 文件内，只需修改这串代码即可。

```
baseUrl = 'http://openlan.missiono.cn'	
```
