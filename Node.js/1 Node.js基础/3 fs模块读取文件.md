### Node.js 1.3 fs模块读取文件内容

1. **fs 文件系统模块**

   fs 模块是用来操作文件的模块，有一系列的方法和属性。如 `fs.readFile()` `fs.writeFile()`。

   

2. **导入 fs 模块**

   使用 fs 模块操作文件前，需要先导入它：

   ```javascript
   const fs = require('fs')
   ```

   require() 方法接受一个字符串，写入一个模块。fs 模块是 node 安装包里就有的。

   

3. **读取指定文件中的内容：fs.readFile() **

   ```javascript
   fs.readFile(path[, options], callback)
   ```

   参数1：必选参数，字符串，表示文件的路径。

   参数2：可选参数，表示以什么编码格式来读取文件。默认值为 utf8。

   参数3：必选参数，文件读取完成后，通过回调函数拿到读取的结果。

   

   例如：以 utf8 的编码格式，读取指定文件的内容，并打印 err 和 dataStr 的值：

   ```javascript
   const fs = require('fs')
   fs.readFile('./files/11.txt', 'utf8', function(err, dataStr){
       console.log(err)
       console.log('-----')
       console.log(dataStr)
   })
   ```

   如果读取成功，err 值为 null。如果读取失败，dataStr 值为 undefined，而 err 值为一个错误对象。

   

4. **判断文件是否读取成功**

   可判断 err 对象是否为 null。`if(err === null){}` 或者 `if (err){return...}` 。这两种写法逻辑相反。

   <font color='red'>注意抛出错误时，err 是错误对象，而 err.message 是基于 err code 的错误信息。</font>

   