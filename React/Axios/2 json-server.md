### Axios 2   json-server

1. **json-server** 

   [json-server](https://github.com/typicode/json-server/tree/1759c986b57302be89742375525d238b3af66039) （[中文文档](https://www.cnblogs.com/fly_dragon/p/9150732.html)）是用来快速搭建 REST API 的工具包。

   

1. **安装步骤**

   1. 全局安装（前提是安装好了node环境） `npm install -g json-server`

      检查是否安装成功：`json-server -h` <font color='lightgrey'>（成功会显示 Option 和 Examples 列表。）[^1]</font>

      <font color='red'>这里注意，如果报错，可以通过代码前加 `npx` 来解决，如</font> `npx json-server -h` <font color='red'>，下同。</font>
   
      
   
   2. 项目根目录下创建一个 db.json 文件，并且复制 json-server 代码[^2]。
   
      
   
   3. 启动服务 `json-server --watch db.json` 
   
      <font color='red'>报错改用</font> `npx json-server --watch db.json` 
   
      启动后点击 http://localhost:3000 等链接就可以看到 db.json 的内容。地址后面加 /posts 或 /comments 或 /profile 可以获得具体的某项内容，再继续添加 /1 或 /2 等数字可以获取内容中 id=? 的数据。
   
      <font color='lightgrey'>这里注意，查询参数有两种方式，即 param `/` 和 query `?`。param `/`后返回的是一个对象（定位处理），而 query `?` 后返回的是一个只有一个元素数组（过滤处理）。</font>





**注释**

[^1]: 不成功的话是 json-server 安装问题

安装问题的解决有3个方法。第一个是代码前加 npx，第二个是在当前目录下开一个cmd然后打代码，第三个是通过管理员模式的 PowerShell 修改权限 [About excution policy](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.2)。

管理员模式 PowerShell：

1. 按 Win + R. 

2. 输入 powershell， 按 Ctrl+Shift+Enter。

3. 点击 OK 即可通过管理员权限开启 PowerShell.

   

[PowerShell](https://so.csdn.net/so/search?q=PowerShell&spm=1001.2101.3001.7020) 默认不允许执行*.ps1脚本文件。运行ps1文件会得到下面的错误:

*File C:\Temp\Test.ps1 cannot be loaded because the execution of scripts is disabled on this system. Please see "get- help about_signing" for more details.*

下面的命令可以解决上面的错误

PS C:\Windows\system32> Set-ExecutionPolicy RemoteSigned  <font color='red'><按回车></font>



[^2]:db.json 代码

```json
{
  "posts": [ //文章，而不是POST请求
    { "id": 1, "title": "json-server", "author": "typicode" }
  ],
  "comments": [
    { "id": 1, "body": "some comment", "postId": 1 }
  ],
  "profile": { "name": "typicode" }
}
```

