### 项目目录

├── bin 发布相关脚本  
├── build 客户端用到的公共依赖  
├── client 客户端代码  
&ensp;&ensp;├── component 通用组件  
&ensp;&ensp;├── constant 常量  
&ensp;&ensp;├── img 图片  
&ensp;&ensp;├── model axios请求  
&ensp;&ensp;├── page 页面  
&ensp;&ensp;└── utils 常用方法  
├── config 项目配置文件  
├── index.js 项目启动文件  
├── lib 服务端使用的一些库文件  
├── mockData 自定义mock数据  
├── package.json  
├── pm2-release.json pm2配置文件（非prod环境）  
├── pm2.json pm2配置文件（prod环境）  
├── server Node服务代码 
├── static 打包后的资源目录  
└── tools 钩子、Plus发布描述文件、alias  

### Web技术栈
* React 不仅仅是UI库
* Redux / Mbox 状态管理
* React-router 前端路由
* Axios 异步请求
* 桥接库（针对移动端）

### Server端技术栈
* Koa Node.js的web框架
* Koa-router 路由
* crypto 加密，做BA认证
* hlb (http loader balancer)公司范围内统一的http服务调用框架，提供http服务治理功能
* thrift Apache RPC通信（最早由facebook研发）
* thriftmap 根据IDL生成文档、Service和Controller的工具

### 构建及发布
* Webpack 模块构建工具

### 服务保障
* PM2 进程管理器，保证在不停机的情况下重启应用
* Sentry 错误日志
* 埋点数据统计 参考google analysis

### 开发流程及质量保证
* 项目开发流程
* 代码审查
* 注释率覆盖
* 静态检查
* 千行Bug率
