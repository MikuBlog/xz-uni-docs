# 常见问题

## IE浏览器发出请求

使用`IE`浏览器发出请求的`url`中文信息将会被乱码处理，如果要将中文参数放置在`url`中，则需要在发送请求前先对`url`进行编码。

解决方案：使用`encodeURI`（只对中文字符进行编码），作者已经在`axios`拦截器中作统一转码，使用`axios`不需要再手动编码。

```js
encodeURI(url)
```

<br/>

## IE浏览器样式出错

`IE10+`会出现样式错乱问题，但总体不影响使用，如有需要，请自行修改样式

<br/>

## 日期格式出错

`IE`浏览器与`IOS`系统的所有浏览器都不支持`new Date('yyyy-MM-hh')`

请将日期格式转化为`new Date('yyyy/mm/hh')`（该日期格式对所有浏览器兼容），防止因日期格式不统一而出现浏览器兼容性问题