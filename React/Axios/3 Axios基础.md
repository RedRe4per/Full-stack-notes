### Axios 3   Axios 基础

1. **Axios** [介绍](https://github.com/axios/axios)

   React 和 Vue 都用 Axios 发送数据请求。

   Axios 可以在浏览器中运行，向服务器端发送 Ajax 请求。

   Axios 也可以在 node.js 中运行，向服务器端发送 http 请求。

   

2. **Axios 特点**

   1. 用于浏览器/node.js，向服务器发送 Ajax/http 请求。

   2. 使用 Promise API。

   3. 请求/响应拦截器。在请求前做准备工作，并且在结果返回时做预处理。

   4. 帮我们对请求和响应数据做转换。

   5. 取消请求。

   6. 自动把结果转成 json 数据。

   7. 阻挡 XSRF 跨站攻击来保护客户端。

      

3. **安装 Axios**

   项目中 `npm install axios` 或 `yarn add axios`

   标签引入 `<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>`

   

4. **基本使用**

   Axios 参数接收一个对象，配置项写在此处。Axios 返回的是一个 Promise 对象，因此用 then( ) 来指定成功的回调来获取结果。

   每个请求发送后都可以通过 Network 来查看请求头信息。

   

   1. GET 请求<font color='lightgrey'>（查询）</font>

      ```javascript
      btns[0].onclick = function(){
          axios({
              method: 'GET',
              url: 'http://localhost:3000/posts/2' //json-server文档中有请求对应的写法
          }).then(response => {
              console.log(response);
          });
      }
      ```

      

   2. POST请求<font color='lightgrey'>（添加一片新的文章）</font>

      ```javascript
      btns[1].onclick = function(){
          axios({
              method: 'POST',
              url:'http://localhost:3000/posts', 
              data: {
                  title:'new article',
                  author:'Tom'
              }
          }).then(response => {
              console.log(response);
          });
      }
      ```

      请求后可以在 db.json 文件中找到发送的数据，因为没有指定 id，所以在 posts 中顺序添加。此外，在Network-Headers 旁边的 Payload 能看到发送的数据。

      

   3. PUT 请求<font color='lightgrey'>（修改数据）</font>

      ```javascript
      btns[2].onclick = function(){
          axios({
              method: 'PUT',
              url:'http://localhost:3000/posts/3', //要在这里指定id，而不是在data中指定。
              data: {
                  title:'second new article',
                  author:'Jonny'
              }
          }).then(response => {
              console.log(response);
          });
      }
      ```

      

   4. DELETE 请求<font color='lightgrey'></font>

      ```javascript
      btns[3].onclick = function(){
          axios({
              method: 'DELETE',
              url:'http://localhost:3000/posts/5' //DELETE请求只需要id，不需要请求体。
          }).then(response => {
              console.log(response);
          });
      }
      ```

      

5. **Axios 其他方法发送请求**

   与Axios.3.4节相比，本节的请求方式只是写法不同。

   ```javascript
   axios.request(config)
   axios.get(url[, config])
   axios.delete(url[, config])
   axios.head(url[, config])
   axios.options(url[, config])
   axios.post(url[, data[, config]])
   axios.put(url[, data[, config]])
   axios.patch(url[, data[, config]])
   ```

   Config就是其他配置项，如请求头和请求体。

   

   例如 .request( ) 

   ```javascript
   btns[0].onclick = function(){
       axios.request({
           method: 'GET',
           url: 'http://localhost:3000/posts/2' 
       }).then(response => {
           console.log(response);
       });
   }
   ```

   .post( )

   ```javascript
   btns[1].onclick = function(){
       axios.post(    //这里没{
           url='http://localhost:3000/posts',    //这里是url=
           {
               title:'new article by .post()',
               author:'Tomas'
           }).then(response => {
           console.log(response);
       });
   }
   ```

   

7. **Axios 响应结构**

   Axios 请求返回的对象，即 then(response) 的结果。

   1. config 是配置对象，包括请求类型，请求url，请求体等。

   2. data 是响应体（服务器返回结果）。它是一个对象，因为 Axios 自动将服务器返回结果 json 解析，方便处理。

   3. headers 是响应头信息。

   4. request 是原生 Ajax 请求对象（XMLHttpRequest() 实例对象）。因为 Axios 是用 Ajax 发送请求。

      status 是响应状态码，statusText 是响应字符串。

![image-20220220213319821](C:\Users\GUOQING ZHU\AppData\Roaming\Typora\typora-user-images\image-20220220213319821.png)
