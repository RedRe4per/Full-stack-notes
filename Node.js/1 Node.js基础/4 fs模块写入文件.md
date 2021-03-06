### Node.js 1.4 fs模块写入文件内容

1. **向指定文件写入内容：fs.writeFile() **

   ```javascript
   fs.writeFile(path, data[, options], callback)
   ```

   参数1：必选参数，字符串，表示文件的路径。

   参数2：必选参数，表示要写入的内容。

   参数3：可选参数，表示以什么编码格式来读取文件。默认值为 utf8。

   参数4：必选参数，文件读取完成后，通过回调函数拿到读取的结果。无论写入成功或者失败都会调用。

   

   例如：以 utf8 的编码格式，读取指定文件的内容，并打印 err 和 dataStr 的值：

   ```javascript
   const fs = require('fs')
   fs.writeFile('./files/12.txt', 'added information', 'utf8', function(err){
       console.log(err)
   })
   ```

   如果写入成功，err 值为 null（因此这里不要直接写 err.message，因为无论成功失败，都会执行回调函数，而成功时没有 message）。

   如果读取失败，err 值为一个错误对象。

   

2. **判断文件是否写入成功**

   根据 err 是否能转成 true：`if(err){return...}` 

   如果 err 能转为 true，即表示 err 对象不是 null，写入失败了。

   

3. **fs.writeFile() 写入的机制**

   fs.writeFile() 写入是替换文件内容，而不是在原有内容中追加。

   当没有指定的文件时，会创建一个新文件，然后写入内容。但是如果没有指定目录，就会报错。

   

4. **向指定文件追加内容 appendFile()**

   ```javascript
   fs.appendFile(filepath, data[, options], callback_function);
   ```

   参数1：必选参数，字符串，表示文件的路径。

   参数2：必选参数，表示要写入的内容。

   参数3：可选参数，表示以什么编码格式来读取文件。默认值为 utf8。

   参数4：必选参数，文件读取完成后，通过回调函数拿到读取的结果。无论写入成功或者失败都会调用。

   基本同 fs.writeFile()。追加的内容不会自动换行或者空格。

   

5. **向指定文件同步追加内容appendFileSync()**

   ```javascript
   fs.appendFileSync(filepath, data[, options]);
   ```

   参数1：必选参数，字符串，表示文件的路径。

   参数2：必选参数，表示要写入的内容。

   参数3：可选参数，表示以什么编码格式来读取文件。默认值为 utf8。

   

