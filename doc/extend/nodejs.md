## Nodejs


* 主流框架：
    express：技术文档成熟
    koa：新语法
    egg：企业大型项目

* 视图模板：
    pug(jade)：写法不像html
    art-template：性能最好
    ejs：功能较少

* 应用：
    搭建全栈：
    模拟数据接口：
    中间层开发：（流程：客户端请求node服务，node服务发出请求，后端返回数据给node服务，node服务生成视图模板字符串给客户端）
        node服务：可以利用redis做缓存，做请求合并，做负载均衡
    制作项目构建工具：webpack、vue-cli

* http：
* https：公钥+私钥
* http2：公钥+私钥，createSecureServer

* node进阶:
    redis缓存设计
    三大框架
    使用数据库
    服务器部署
    项目开发实战
