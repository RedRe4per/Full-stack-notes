### Axios 1   http

1. **http基础**

   client 给 server 发送请求（请求报文），请求内容包括 *请求行、请求头、和请求体*。

   server 响应 client 返回数据，http 响应（响应报文）包括 *状态行、响应头、实体内容*。

   

   请求具体内容，在 inspect-network 里面查看。其中 All-Name 下的第一个项（网址项）就是发送到请求。点开以后的 Headers 中有 General，Response Headers 和 Request Headers，<font color='red'>这些是浏览器整理过的信息</font>。

   ![image-20220220133840118](C:\Users\GUOQING ZHU\AppData\Roaming\Typora\typora-user-images\image-20220220133840118.png)

   请求报文：

   1. 请求行

      method url

      GET/<font color='lightgrey'>produc_detail?id=2</font>

      POST/<font color='lightgrey'>login</font>

   2. 多个请求头

      Host: www.google.com

      Cookie[^1]: <font color='lightgrey'>SEARCH_SAMESITE=CgQIl5QB; HSID=Acx6gym1ffa3ppTqI; SSID=ABqoRPct1dz_XB-1y; ...</font> 

      Content-Type: apllication/x-www-form-urlencoded 或 application/json

      ​		Content-type是请求体内容类型。

   3. 请求体

      请求体不一定有。GET请求时无请求体，POST请求[^2]不带参数无请求体，POST请求带参数有请求体。

      username=tom&pwd=123   <font color='lightgrey'>这是 Content-Type: apllication/x-www-form-urlencoded 格式。</font> 

      {"username": "tom", "pwd": "123"}   <font color='lightgrey'>这是 Content-Type: application/json 格式。</font> 

      

   响应报文：

   1. 响应状态行

      status 状态码，如200，201，401，404，500。<font color='lightgrey'>（与status text例一一对应）</font> 

      statusText 状态文本，如OK，Created，Unauthorized，Not Found，Internal Server Error 

   2. 多个响应头

      Content-Type: text/html; <font color='lightgrey'>（html格式文本，如果是JSON格式为 text/json）</font> charest=utf-8  <font color='lightgrey'>（编码）</font>

      Set-Cookie: BD_CK_SAM=1; path=/  <font color='lightgrey'>服务器携带 Cookie 数据返回，对应请求头中的Cookie。</font>

   3. 响应体

      html 文本/json 文本/js/css/图片..

   

2. **不同类型的请求及作用**

   同一个服务器地址，发送不同类型的请求，服务器做的事情不一样。

   1. GET：从服务器端读取数据
   2. POST：向服务器端添加新数据
   3. PUT：更新服务器端已有数据 （实际中经常和 POST 混着用）
   4. DELETE：删除服务器端数据

   

3. **Ajax请求**

   发送 Ajax 请求有两种方式：XHR 对象，fatch( ) 函数。

   

4. **API 的分类**

   此处的 API 指的是前后台交互的接口。

   1. REST API：restful <font color='lightgrey'>（别称）</font>

      1. 发送请求进行 CRUD <font color='lightgrey'>（CRUD：增删改查的英文缩写，create/read/update/delete）</font>中哪个操作由请求方式来决定

         <font color='lightgrey'>其实就是Axios.1.2节中的不同类型请求。如果服务器支持不同请求类型对应不同操作，即为restful；反之为restless。</font>

      2. 同一个请求路径可以进行多个操作

      3. 请求方式会用到 GET/POST/PUT/DELETE

   2. 非 REST API： restless <font color='lightgrey'>（别称）</font>

      1. 请求方式不决定请求的 CRUD 操作
      2. 一个请求路径只对应一个操作
      3. 一般只有 GET/POST <font color='lightgrey'>（GET做查询，POST做增删改）</font>





**注释**

[^1]: [Cookie 介绍](https://blog.csdn.net/weixin_42220532/article/details/103129380)

1. 基本特点：1. cookie把数据存储在客户端浏览器，以key=value的形式。2. 浏览器对于单个Cookie的大小有限制（4kb），对同一域名下Cookie的数量也有限制。

2. 应用：1. 由于Cookie是存在浏览器中的，相对来说是不安全的，所以用来存储一些不敏感的数据。2. 主要应用是在不登陆的情况下，完成服务器对客户端的身份识别，保存用户的一些设置。



[^2]: Post 请求参数格式

1. Content-type: application/x-www-form-urlencodedl charest=utf-8

​		用域键值对参数，参数的键值用=连接，参数之间用&连接。

​		例如：name=%E5%B0%8F%E6%&age=12

2. Content-Type: application/json; charset=utf-8

   用于json字符串参数。

   例如：{"name": "%E5%B0%8F%E6%", "age": 12}

3. Content-Type: multipart/form-data 

   上传文件等。



