# 前端部署

## 项目打包

如果未安装`HbuilderX`，请[点击此处前往下载编译器](https://www.dcloud.io/hbuilderx.html)

选择左上角菜单选择发行对应端的代码进行编译打包即可

> 建议安装`finalshell`，一款服务器可视化工具，方便管理自己的服务器。

### window

- 到`nginx`官网下载`window`版压缩包（作者使用的是`nginx-1.14.2`）

> http://nginx.org/en/download.html

- 在任意位置解压`nginx`压缩包

- 进入`nginx`根目录，并在`html`目录下新建一个文件夹`admin`文件夹

- 回到`nginx`根目录，并进入到`conf`目录下，找到`nginx.conf`并打开

- 找到`http`域并另起一行，加入如下代码：

```
sever {
  listen 80;
  server_name xxx.com;#(您的域名)
  location / {
    root html/admin;
		try_files $uri $uri/ /index.html;
		index index.html;
  }
}
```

- 回到`nginx`根目录，双击`nginx.exe`运行`nginx`

### linux

- 安装`nginx`

  - 配置`nginx`安装仓库

  ```
  vim /etc/yum.repos.d/nginx.repo
  ```

  - 填入配置信息并保存退出(`:wq`命令)

  ```
  [nginx]
  name=nginx repo
  baseurl=http://nginx.org/packages/centos/7/$basearch/
  gpgcheck=0
  enabled=1
  ```

  - 下载并安装`nginx`

  ```
  yum install nginx
  ```

  - 检查是否安装成功

  ```
  nginx -v
  ```

  - 如果有显示版本信息，那么则安装成功。作者提示的信息如下（现在最新版本为1.16.x）：

  ```
  nginx version: nginx/1.14.0
  ```

- 配置`nginx`

  - 进入到配置文件目录下

  ```
  cd /etc/nginx/conf.d
  ```

  - 新建服务器文件

  ```
  touch admin.conf
  ```

  - 配置`admin.conf`文件

  ```
  vim admin.conf
  ```

  - 填入如下配置内容：

  ```
  server {
    listen 80;
    server_name xxx.com;#(您的域名)
    location / {
      root /usr/share/nginx/admin;
      try_files $uri $uri/ /index.html;
      index index.html;
    }
  }
  ```

- 新建前端静态文件目录
   
  - 进入到如下目录：

  ```
  cd /usr/share/nginx
  ```

  - 创建`admin`文件夹：

  ```
  mkdir admin
  ```

  - 进入到`admin`文件夹目录下：

  ```
  cd admin
  ```

- 将打包好的文件上传至该文件夹里，`admin`内文件目录如下：

```
├─assets
│  ├─css
│  ├─images
│  └─js
├─css
├─fonts
├─img
├─js
└─ueditor
```

> 如果使用finalshell，则可直接拖拽文件上传，否则请使用linux第三方上传工具进行远程上传

- 重启`nginx`

```
nginx -s reload
```

<br/>

> 打开浏览器输入您的域名，按下回车键，开始你的愉快分享之旅吧！

<br/>
<br/>

## 配置nodejs

- 回到服务器根目录

- 下载`node.js`

```
wget https://npm.taobao.org/mirrors/node/v12.4.0/node-v12.4.0-linux-x64.tar.xz
```

- 解压

```
tar -xvf node-v12.4.0-linux-x64.tar.xz
```

- 进入`bin`目录

```
cd node-v12.4.0-linux-x64/bin
```

- 测试

```
./node -v # 如果出现版本号即安装成功
```

- 关联并全局使用

```
ln -s /node-v12.4.0-linux-x64/bin/node /usr/local/bin/node

ln -s /node-v12.4.0-linux-x64/bin/npm /usr/local/bin/npm
```

<br/>
<br/>

## 配置cnpm

- 安装`cnpm`(前提是已经安装好`node`并全局关联)

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

- 关联`cnpm`

```
ln -s /node-v12.4.0-linux-x64/bin/npm /usr/local/bin/cnpm
```

<br/>
<br/>

## 配置gzip

<br/>

> 配置gzip后，静态文件将被压缩成更小的文件，大大提升浏览器访问静态文件的速度。

- 打开`nginx.conf`，并在`http`模块任意行加入如下代码：

```
gzip on;
gzip_types application/javascript text/plain application/x-javascript text/css application/xml text/javascript application/x-httpd-php image/jpeg image/gif image/png application/json;
```

- 保存并重启`nginx`

`window`与`linux`的配置方式完全一致，只需要找到`nginx.conf`配置文件进行如上操作即可

<br/>
<br/>

## 负载均衡

> 有效处理服务器高并发，同时也适用于平滑部署

- 打开`nginx.conf`，并在`http`模块任意行加入如下代码：

```
upstream xuanzai {
	server xxx.com weight=10; # 服务器1
	server xxx.com weight=10; # 服务器2
}
```

- 配置`server`模块

```
server {
	listen 80;
	server_name xzadmin.xuanzai.top; # 暴露给用户访问的域名
	location / {
		proxy_pass http://xuanzai; # 名称与负载均衡配置的名称一致
		proxy_redirect default;
		index index.html;	
		root html;
	}	
}
```

- 保存并重启`nginx`

这样，简单的负载均衡就配置完成了！<br/>
此时如果两个（或多个）服务器已开启，那么可尝试访问已配置好的域名，查看是否配置成功<br/>
`window`与`linux`的配置方式完全一致，只需要找到`nginx.conf`配置文件进行如上操作即可

<br/>

- 平滑部署

> 如果没有使用服务器负载均衡，那么每次部署都势必会影响用户的访问。使用了负载均衡，则在部署期间可逐个服务器部署而不影响用户的使用体验。（部署前先停止该服务器的运行`nginx -s stop`，否则用户访问便可能会报502、404等类似的错误）

<br/>
<br/>