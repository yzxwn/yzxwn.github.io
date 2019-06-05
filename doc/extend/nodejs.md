## Nodejs


* 主流框架：
    express：技术文档成熟
    koa：新语法、更轻更灵活、可扩展
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

* 负载均衡：
    负载均衡器 Nginx：一个高性能的web服务器和反向代理服务。用户请求先到Nginx，再由Nginx转发请求到后面的应用服务器
        一般做到10万并发，更大并发使用Nginx集群，负载均衡器 LVS（Linux虚拟服务器），F5，DNS域名服务器
        启动（start nginx）、关闭（nginx -s stop）、重启（nginx -s reload）
        监听本地端口，域名解析，配置服务器集群

* node进阶:
    redis缓存设计：如果数据是最新的则从redis存储中获取数据，否则向后端请求最新数据
        安装redis服务：
            下载redis安装包、开启redis服务、修改配置文件
            五种数据类型：string（变量）、hash（对象）
        在node中使用：安装redis库、引入redis库、创建redis.createClinent客户端、存取数据（异步回调）
            按页面划分缓存hash
    三大框架
    使用数据库
    服务器部署
    项目开发实战
