# 快速开始

## 运行项目

新建一个文件夹，在该目录下直接使用如下命令
```
git clone https://github.com/MikuBlog/xz-admin.git
```

进入到下载好的项目目录下，使用如下命令进行依赖安装
```
npm install
```

在项目根目录下执行以下命令运行项目
```
npm run serve
```

## 目录结构

```
├─api // 存放自行封装的api
│  ├─database
│  ├─dom
│  ├─file
│  ├─http
│  ├─iconfont
│  ├─json
│  ├─message
│  ├─other
│  └─storage
├─assets // 静态资源文件
│  ├─error
│  ├─loading
│  ├─login
│  ├─logo
│  └─welcome
├─components // 第三方与自行封装的组件
│  ├─breadcrumb
│  ├─editor
│  ├─icon_select
│  ├─scrollpane
│  ├─search_menu
│  ├─SvgIcon
│  ├─tag
│  ├─tree_menu
│  └─tree_table
├─global // 全局模块
│  ├─css
│  └─js
├─icons // 存放SVG图标
│  └─svg
├─initial // 第三方插件、过滤器、自定义指令、样式初始化
│  └─UI
├─Layout // 布局组件
├─router // 路由模块
├─store // vuex
│  └─modules
├─utils // 工具类函数
└─views // 页面
    ├─article
    ├─chart
    │  ├─js
    │  └─style
    ├─common
    │  ├─editor
    │  ├─file
    │  ├─icon
    │  │  ├─js
    │  │  └─style
    │  └─markdown
    │      └─js
    ├─docs
    ├─error
    ├─introduction
    ├─Layout
    │  ├─components
    │  ├─js
    │  └─style
    ├─log
    │  ├─authority_log
    │  │  ├─components
    │  │  └─js
    │  ├─exception_log
    │  │  └─js
    │  └─operation_log
    │      └─js
    ├─login
    │  ├─js
    │  └─style
    ├─menu_1
    ├─menu_2
    ├─menu_3
    ├─monitor
    │  ├─online_user
    │  │  └─js
    │  └─redis_manage
    │      └─js
    ├─order
    ├─person
    │  └─components
    ├─system
    │  ├─authority
    │  │  ├─components
    │  │  └─js
    │  ├─department
    │  │  ├─components
    │  │  └─js
    │  ├─dictionary
    │  │  ├─components
    │  │  └─js
    │  ├─menu
    │  │  ├─components
    │  │  └─js
    │  ├─role
    │  │  ├─components
    │  │  └─js
    │  ├─station
    │  │  ├─components
    │  │  └─js
    │  └─user
    │      ├─components
    │      └─js
    ├─tools
    │  ├─file
    │  │  └─components
    │  ├─generator
    │  │  ├─components
    │  │  └─js
    │  ├─mission
    │  │  ├─components
    │  │  └─js
    │  └─picture
    │      ├─components
    │      └─js
    └─welcome
```

## 页面模块结构

为了方便后期的开发与维护，本后台管理系统模板对每个页面模块拆分成如下结构：

```
│  ├─menu // 页面模块名称
│  │  ├─components // 页面组件
│  │  └─scss // 页面样式
│  │  │  └─index.scss
│  │  └─data // 静态数据模块
│  │  └─js // 业务逻辑模块
│  │  │  └─initial.js // 初始化文件
│  │  │  └─operation.js // 页面逻辑文件
│  │  │  └─property.js // 响应式属性管理文件
│  │  ├─index.vue // 页面
```

当然，怎么开发舒爽怎么来也是没问题的~~~
