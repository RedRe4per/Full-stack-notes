### React Appendix 1   报错分析

1. **手动引入React库的警告**

   <font style="background-color:yellow;">You are using the in-brower Babel transformer. Be sure to precompile your scripts for production - </font>

   初学者使用手动引入React库的方法时，浏览器拿到 script 代码时才发现不是JS，要靠 babel 然后浏览器现场翻译。当代码多的时候会白屏，等待后才能运行。因此会出现黄色警告。

   <font style="background-color:pink;">Failed to load resource: the server responded with a status of 404 (Not Found)</font>

   网站没有图标，刷新后就没了。

   

2. **网站图标**

   无图标的时候控制台会报错，刷新后解除。

   <font style="background-color:pink;">Failed to load resource: the server responded with a status of 404 (Not Found)</font>

   解决方法：制作一个名称/格式为 favicon.ico的图标，放入根目录。

   强制刷新后就会出现图标。<font color='red'>强制刷新：按住shift+刷新。</font>



3. **a.b 结构分析错误点**

   写出 `this.state` 后，可能会报错：<font style="background-color:pink;">Cannot read property 'state' of undefined</font>。意为不能在 undefined 上读取 state。即 `this.state` 中，this指向为undefined。同理，类似的报错中，直接去寻找 `a.b` 结构中的 `a` 错误即可。
   
   

4. **React 把对象作为节点的错误**

   <font color='red'>React不能直接把对象当作一个节点写在JSX标签中。</font>对应报错为：

   <font style="background-color:pink;"> Uncaught Invariant Violation: Objects are not valid as a React child. If you meant to render a collection of children, use an array instead. </font>
   
   

5. **组件名没大写**

   <font color='red'>组件名必须大写。</font>如果组件名小写的话，用小写名渲染后会报错：

   <font style="background-color:pink;"> Warning: Function are not valid as a React Child. This may happen if you return a Component instead of <Component /> from render. Or maybe you meant to call this function rather than return it. </font>

   

6. **跨域**

   如果不配置代理，会发生跨域问题（<font color='red'>No 'Access-Control-Allow-Origin' header...</font>）。跨域的原因是，Client 的地址是 http://localhost:3000 ，而服务器地址是 http://localhost:5000 ，因此 ajax 请求不允许。

   

7. **Axios 返回 error 没反应**

   <font color='red'>Axios 返回的错误是 error.message 而不是 error</font>

   如果用的是 error，会一直报错：<font style="background-color:pink;"> Objects are not valid as a React child </font>。这个错误的意思是，JSX 中 {} 中必须是 string 或者 array，<font color='red'>而不能是对象</font>。而 Axios 返回的 error 是一个对象，无法通过 JSX 呈现到页面（但是可以在 Console 中显示），因此只能用 error.message。<font color='lightgrey'>message 不要拼错成 massage。</font>

   

8. **render( )中几种错误写法**

   1. `<h1 onClick={changeWeather}> ` 这种会报错 <font style="background-color:pink;">  changeWeather is not defined </font>。这是因为只有实例可以调用类中的函数，按照逻辑要写成 <font color='red'>this</font>.changeWeather 才能找得到。

   2. `<h1 onClick={this.changeWeather}> ` 这种会报错 <font style="background-color:pink;">  cannot read property 'state' of undefined </font>。这说明 state 的左边又出错了，即 this 指向 undefined。这是什么原因呢？<font color='lightgrey'>（本错误仅限于使用构造器/普通函数才会出现。使用非构造器的箭头函数写法时没有这个问题）</font>

      

9. **state 中 key-value 对写错**

   这里要注意，state 中状态只有 {} 对象写法，而对象中的数据全都是 key-value 对，写作 key: value。如果 key: value 写作了 key=value，会报错，即 <font style="background-color:pink;"> Parsing error: Invalid shorthand property initialiser.</font>
   
   

10. **路由链接和路由组件的两种报错@5版本**

    直接写 `<Link>` 会报错：<font color='brown'>Error: Invariant failed: You should not use `<Link>` outside a `<Router>`</font>。因为路由链接和路由都要收到路由器的管理，即 `<Link>` 外侧要包一个 `<Router>`。

    并且，<font color='red'>使用 `<Router>` 包裹 `<Link>` 时要指定 Router 类型：`<BrowserRouter>` / `<HashRouter>`</font>。否则会报错：<font color='brown'>TypeError: Cannot read property 'location' of undefined</font>。

    如果是路由组件外没包裹 `<BrowserRouter>` / `<HashRouter>`，报错会类似，只是 `<Link>` 变为 `<Route>`。

    以上是react-router-dom 5版本，如果是6版本的话，外面包裹 `<Routes>`。

    

11. **路由链接和路由组件@6版本错误**

    <font style="background-color:pink;"> Uncaught Error: [App] is not a  <Route> component. All component children of <Routes> must be a <Route> or <React.Fragment></font> 解决方法应该同上，但是用6版本。



12. **样式丢失**

    样式丢失触发条件：导航链接用了 /a/b 这种多/的（非嵌套路由）并且用了 bootstrap，网页呈现后刷新，就可能丢失样式。（新版本应该已修复）每次刷新可用按住 SHIFT 再刷新，强制刷新不走缓存。

    原因分析：在network中，寻找 bootstrap.css 文件，status是200（成功），这里样式没丢。这里点开后找到 bootstrap.css 地址 http://localhost:3000/css/bootstrap.css 。这就是脚手架中 bootstrap.css 的地址。（其中  http://localhost:3000 是脚手架内置服务器（webpack 中 devServer 创建的），public 就是  http://localhost:3000 的根路径。）bootstrap.css 地址有效性的验证可以靠直接在浏览器中看这个地址，或者 network 中 header 旁边的 response。

    但是当用了 /a/b 结构后，bootstrap.css 文件，status是304。点开后发现地址为 http://localhost:3000/a/css/bootstrap.css ，即 /a/b 结构中的 /a 被认为是根路径的一部分了，因此 css 文件地址错误。这时 response 里返回的是 index.html。这是因为<font color='red'>脚手架中有一个机制，即如果用地址请求了一个不存在的资源，脚手架会把 public 中的 index.html 呈现出来。</font>这里报错为 <font style="background-color:yellow;">Resource interpreted as Stylesheet but transferred with MIME type text/html: "http://localhost:3000..." </font>

    解决方案有三种：

    1. 在 public 的 index.html 中， css引入路径把 `href='./css/bootstrap.css'` 改为 `href='/css/bootstrap.css'` （去掉 `.`）。这里的原理是把 `./` 的相对路径改成了 `/` 的绝对路径。`/` 意为直接去 http://localhost:3000 请求内容。一般都是用这种。

    2. index.html 中， css引入路径改为 `href='%PUBLIC_URL%/css/bootstrap.css'` 。%PUBLIC_URL% 代表 public 文件的绝对路径。此方案仅限于 React 脚手架。

    3. src 下 index.js 中，BrowerRouter 改为 HashRouter。改后根路径就变成了 http://localhost:3000/#/ 。#后都被认为是前端资源，不带给服务器，如 http://localhost:3000/#/a/b 。

       

13. 