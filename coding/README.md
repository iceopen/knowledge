# 开发相关规范 Coding

## 服务运行

* [运行说明](system-runtime.md)

## 规范

* [RESTful API 设计指南](restful-api.md)
* [理解OAuth 2.0](oauth2.0.md)

## 常见程序漏洞说明

- 1.功能暴露查询和操作类，没有进行绑定效验、登录效验。
- 2.短信没有进行发送数量和速度限制

## 开发语言说明

- Node.js 主要做前端展示开发、前后端分离
- Golang 主要做前端展示、后端开发、restful 网关

### 技术栈选择说明

#### Node.js

- 开发者工具：webstorm / VScode
- Mvc 框架选择上：express 4+
- 常用模块：express-session、ejs、vue 2+、log4js、request 等

#### Golang
在 *Golang* 开发技术栈上建议使用，对应语言开发软件例如：队列使用NSQ、数据库使用TIDB、负载均衡Træfɪk、容器管理Kubernetes等技术链

- 开发者工具：Gogland / VScode
- Mvc 框架选择上：Beego / Gin
- ORM ：Beego / Gorm
- [Golang 文件名命名规则](golang.md)