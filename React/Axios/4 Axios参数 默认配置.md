### Axios 4   Axios参数（配置对象）默认配置

1. 配置对象 Request Config

   这些配置对象不仅可以用在 axios( )，也可以用在 .request( )，.post( )等请求方法。

   ```javascript
   {
     // 服务器url地址
     url: '/user',
   
     // 请求方式
     method: 'get', // 默认为get
   
     // 设定url的基础结构，比如http、localhost、3000等。设置baseURL后只需要再写后续路径即可。
     baseURL: 'https://some-domain.com/api/',
   
     // 处理请求数据，处理后再向服务器发送。即预处理请求参数。
     transformRequest: [function (data, headers) {
       	// Do whatever you want to transform the data
       return data;
     }],
   
     // 即预处理响应结果。
     transformResponse: [function (data) {
       	// Do whatever you want to transform the data
       return data;
     }],
   
     // 配置请求头信息。某些项目进行身份校验时，要求在请求头信息中加入特殊标识，来判断请求是否满足条件。
     headers: {'X-Requested-With': 'XMLHttpRequest'},
   
     // 设定url参数。配置的是一个对象，写各种参数。比在url中写可读性强。
     params: {
       ID: 12345
     },
   
     // 参数序列化配置项，不常用。对请求参数序列化并转换成字符串。（服务器端要求数据格式不同时用此配置）
     paramsSerializer: function (params) {
       return Qs.stringify(params, {arrayFormat: 'brackets'})
     },
   
     // 请求体设置（对象形式）。Axios会将其转成json格式字符串传递。按照项目要求选择形式。
     data: {
       firstName: 'Fred'
     },
     
     // 请求体设置（字符串形式）。axios会将其直接传递。按照项目要求选择形式。
     data: 'Country=Brasil&City=Belo Horizonte',
   
     // 超时时间。发送请求后超过此时间，请求就会取消。
     timeout: 1000, // default is `0` (no timeout)
   
     // 跨域请求时对Cookie携带的设置。
     withCredentials: false, // default
   
     // 请求适配器设置。一种是浏览器中Ajax，一种是Node.js中发送http。
     adapter: function (config) {
       /* ... */
     },
   
     // 对请求的基础验证，不常用
     auth: {
       username: 'janedoe',
       password: 's00pers3cret'
     },
   
     // 响应结果格式设置
     responseType: 'json', // default
   
     // 响应结果编码，字符集设置。
     responseEncoding: 'utf8', // default
   
     // 跨域请求标识。对Cookie名字设置。
     xsrfCookieName: 'XSRF-TOKEN', // default
   
     // 跨域请求标识。对请求头信息设置。
     xsrfHeaderName: 'X-XSRF-TOKEN', // default
     /*以上两个是一种安全设置。保证请求来自于自己客户端而不是未知页面，是一种保护作用。因为服务器在返回结果
     会返回一个唯一的标识，下次再发送请求时要把标识发送过去，服务器校验后才会相应。但是某些网页里会加入一些链
     接，向服务器去发送请求。如果不加这两个唯一标识，可能网页链接的请求会对服务器返回结果造成影响。加入了这两
     个标识后，只有客户端发送有标识，其他网页无标识，因此可以避免跨站攻击。*/
   
         
     // 上传时回调
     onUploadProgress: function (progressEvent) {
     },
   
     // 下载时回调
     onDownloadProgress: function (progressEvent) {
     },
   
     // http响应体最大尺寸
     maxContentLength: 2000,
   
     // 请求体最大内容
     maxBodyLength: 2000,
   
     // 对响应结果的成功条件进行设置。不用改，除非自己设置了成功/失败规则。
     validateStatus: function (status) {
       return status >= 200 && status < 300; // default
     },
   
     // 最大跳转次数。发送的服务器请求可能有跳转。一般是只用在Node.js中，Ajax用不到。
     maxRedirects: 5, // default
   
     // 设定socket文件位置，作用是向docker.sock进程发送请求，即数据转发。与proxy有优先级关系。如果设置
     // socket，也设置了代理，优先使用socket。
     socketPath: null, // default
   
     // 客户端信息设置，设置是否保持连接，不常用。
     httpAgent: new http.Agent({ keepAlive: true }),
     httpsAgent: new https.Agent({ keepAlive: true }),
   
     // 设置代理。常用于node.js中，如爬虫请求中切换client地址。
     proxy: {
       protocol: 'https',
       host: '127.0.0.1',
       port: 9000,
       auth: {
         username: 'mikeymike',
         password: 'rapunz3l'
       }
     },
   
     // ajax请求取消设置
     cancelToken: new CancelToken(function (cancel) {
     }),
   
     // an alternative way to cancel Axios requests using AbortController
     signal: new AbortController().signal,
   
     // 响应结果解压，只有node.js用。
     decompress: true // default
   
     // `insecureHTTPParser` boolean.
     // Indicates where to use an insecure HTTP parser that accepts invalid HTTP headers.
     // This may allow interoperability with non-conformant HTTP implementations.
     // Using the insecure parser should be avoided.
     // see options https://nodejs.org/dist/latest-v12.x/docs/api/http.html#http_http_request_url_options_callback
     // see also https://nodejs.org/en/blog/vulnerability/february-2020-security-releases/#strict-http-header-parsing-none
     insecureHTTPParser: undefined // default
   
     // transitional options for backward compatibility that may be removed in the newer versions
     transitional: {
       // silent JSON parsing mode
       // `true`  - ignore JSON parsing errors and set response.data to null if parsing failed (old behaviour)
       // `false` - throw SyntaxError if JSON parsing failed (Note: responseType must be set to 'json')
       silentJSONParsing: true, // default value for the current Axios version
   
       // try to parse the response string as JSON even if `responseType` is not 'json'
       forcedJSONParsing: true,
       
       // throw ETIMEDOUT error instead of generic ECONNABORTED on request timeouts
       clarifyTimeoutError: false,
     }
   }
   ```
   
   

2. **Axios 默认配置**

   实用技巧，可以把重复配置设置在默认配置中，以简化代码。`axios.default.[config]`
   
   Axios 参数（即配置对象）都可以做默认配置。
   
   
   
   不做默认配置时代码如下，每次发送 axios 请求都要设置 method 和 url。
   
   ```javascript
   btns[0].onclick = function(){
       axios({
           method: 'GET',
           url: 'http://localhost:3000/posts' 
       }).then(response => {
           console.log(response);
       });
   }
   ```
   
   做默认配置后，
   
   ```javascript
   axios.default.method = 'GET';
   axios.default.baseURL = 'http://localhost:3000';
   
   btns[0].onclick = function(){
       axios({
           url: 'posts' 
       }).then(response => {
           console.log(response);
       });
   }
   ```
   
   

