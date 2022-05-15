### Node.js 4.1 Express 基础

1. **Express 简介**

   [Express](https://www.expressjs.com.cn/) 是基于 Node.js 平台，快速、开放、极简的 Web 开发框架。Express 的作用和 Node.js 内置的 http 模块类似，是专门用来创建 Web 服务器的。

   Express 的本质：就是一个 npm 上的第三方包，提供了快速创建 Web 服务器的便捷方法。

   如果不使用 Express，就需要用原生 http 模块即可。但 http 内置模块用起来很复杂，开发效率低；Express 是基于内置的 http 模块进一步封装出来的，能够极大的提高开发效率（类似 Web API 和 jQuery 的关系）。

   

2. **Express 能做什么**

   对于前端程序员来说，常见的两种服务器是：

   1. <font color='green'>Web 网站服务器</font>：专门对外提供 Web 网页资源的服务器。
   2. <font color='green'>API 接口服务器</font>：专门对外提供 API 接口的服务器。

   Express 可以快速方便的创建这两种服务器。

   

3. **安装 Express**

   终端命令：`npm i express@4.17.1` （课程中版本）

   

4. **创建 Web 服务器**

   ```javascript
   const express  = require('express')
   const app = express()
   
   app.listen(80, () => {
       console.log('express server running at http://127.0.0.1')
   })
   ```

   

5. **监听 GET/POST 请求**

   通过 `app.get()` `app.post()`方法，可以监听客户端的 GET 请求。

   ```javascript
   app.get('请求URL', function(req, res){})
   app.post('请求URL', function(req, res){})
   ```

   

6. 