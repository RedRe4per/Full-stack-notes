### Node.js 1.8 http模块 创建web服务器 根据url响应不同内容

1. **http 模块**

   http 模块是 Node.js 官方提供的，用来创建 web 服务器的模块。通过 `http.createServer()` 方法，就能方便的把一台普通的电脑变成一台 Web 服务器，从而对外提供 Web 资源服务。

   服务器和普通电脑的区别在于，服务器上安装了 web 服务器软件，如 IIS 和 Apache 等。在 Node.js 中，我们不需要使用 IIS 和 Apache 等<font color='red'>第三方 web 服务器软件</font>。因为可以借助 http 模块来手写服务器软件，并对外提供 web 服务。

   

2. **导入 http 模块**

   ```javascript
   const http = require('http')
   ```

   

3. **服务器相关概念**

   1. IP 地址：可以在 terminal 中通过 `ping 域名` 来获得。浏览器中输入 127.0.0.1，即可把自己电脑当作服务器来访问。

   2. 域名与域名服务器：域名（Domain Name）是与 IP 地址一一对应的字符串，这份对应关系存放在域名服务器（DNS，Domain name server）中。

   3. 端口号：在一台电脑中可能有多干个 web 服务，<font color='red'>每个 web 服务都对应一个唯一的端口号</font>。client 的网络请求会通过端口号交给对应的 web 服务处理。在实际应用中，<font color='red'>url 中的80端口可以被省略</font>。

      

4. **创建 web 服务器**

   步骤

   1. 导入 http 模块

      ```javascript
      const http = require('http')
      ```

   2. 创建 web 服务器实例

      调用 http.createServer() 方法，即可快速创建一个 web 服务器实例。

      ```javascript
      const server = http.createServer()
      ```

      

   3. 为服务器绑定 request <font color='red'>事件</font>，监听客户端请求。

      使用服务器实例的 <font color='green'>`.on()` 方法</font>，为服务器绑定 <font color='green'>request 事件</font>。只要有客户端向服务器发送请求，就会触发 request 事件，从而调用事件处理函数。

      ```javascript
      server.on('request', (req,res)=>{
          console.log('client visit our web server.')
      })
      ```

      

   4. 启动服务器

      调用服务器实例的 `.listen()` 方法，即可启动当前 web 服务器实例。第一个参数为端口号，启动成功后会调用参数2（回调函数）。

      ```javascript
      server.listen(80, ()=>{
          console.log('http server running at http://127.0.0.1')
      })
      ```

      停止服务器用 CTRL+C。同脚手架。

      服务器修改代码后，要重新启动服务器才能让代码生效。

      

5. **req 请求对象**

   只要服务器接收到了客户端的请求，就会调用 `server.on()` 为服务器绑定的 request 事件处理函数。

   如果想在事件处理函数中，<font color='red'>访问与客户端相关的数据或属性</font>，就可以使用 [req 请求对象](https://www.jc2182.com/nodejs/nodejs-req.html)：

   `req.url` ：客户端请求的 url 地址（不是客户端地址，而是想请求的目标地址。地址也不是完整地址，而是从端口号后面的部分开始算。）

   `req.method ` ：客户端的 method 请求类型（GET，POST等）

   

6. **res 响应对象**

   在服务器的 request 事件处理函数中，<font color='red'>如果想访问与服务器相关的数据或属性</font>，就可以使用 res 响应对象。例如客户端在访问服务器后，如果想在客户端的网页上显示服务器内容，就需要用 res 响应对象。

   res 响应对象在回调函数的形参中是第二位，如果想只用 res 不用 req，也需要补全 req。

   `res.end()` 参数是一个 string，向客户端发送字符串。

   

7. **解决中文乱码问题**

   当调用 `res.end()` 方法，向客户端发送中文内容的时候，会出现乱码问题。这时要手动设置编码格式。

   ```javascript
   res.setHeader('Content-Type', 'text/html; charset=utf-8')
   ```

   两个参数都是固定写法。

   

8. **根据不同url响应不同内容**

   步骤：

   1. 获取请求的 ur l地址

   2. 设置默认相应内容为 404 Not found

   3. 判断用户请求是否为 `/` 或 `/index.html` 首页

   4. 判断用户请求是否为 `/about.html` 页面

   5. （如果涉及中文，）设置 `Content-Type` 响应头，防止中文乱码

   6. 使用 `res.end()` 把内容响应给 client

      

   代码实现：

   ```javascript
   const http = require('http')
   const server = http.createServer()
   
   server.on('request', function(req, res){
       const url = req.url
       let content = '<h1> 404 Not Found! </h1>'
       if (url === '/' || url === '/index.html'){
           content = '<h1> main page <h1>'
       }else if (url === '/about.html'){
           content = '<h1> about page <h1>'
       }
       res.setHeader('Content-type', 'text/html; charset=utf-8')
       res.end(content)
   })
   
   server.listen(80, ()=>{
       console.log('server running at http://127.0.0.1')
   })
   ```

   

