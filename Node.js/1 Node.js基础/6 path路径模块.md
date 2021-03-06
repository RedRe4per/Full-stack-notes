### Node.js 1.6 path路径模块

1. **path 路径模块**

   path 模块是 Node.js 官方提供的，用来处理路径的模块。它有处理路径的方法，如 `path.join()` 方法拼接路径， `path.basename()` 解析文件名等。

   

2. **导入 path 模块**

   ```javascript
   const path = require('path')
   ```

   

3. **路径拼接：path.join()**

   `path.join()` 方法可以把多个路径片段拼接为完整的路径字符串。

   ```javascript
   path.join([...paths])
   ```

   参数 ...paths 是字符串类型，为路径片段的序列。返回值是拼好的路径字符串。

   但是路径片段中，要注意 `../` 会导致上一层路径被抵消。而 `./` 不会抵消上一级路径。如果需要抵消上两层路径，应该用 `../../` 。

   ```javascript
   const pathStr = path.join('/a', '/b/c', '../', './d', 'e')    //结果为 \a\b\d\e
   const pathStr2 = path.join(__dirname, './files/1.txt')    //可以拼接出完整的绝对路径。
   ```

   

   <font color='red'>今后涉及到路径拼接的操作，都要使用 `path.join()` 方法处理，不要使用 `+` 进行字符串拼接。</font>原因是如果多谢了一个 `.` 如 `./` ，使用加号拼接后路径会错误。但是 `path.join()` 会处理掉多余的 `.` 。

   ```javascript
   fs.readFile(path.join(__dirname, '/files/1.txt'), 'utf8', function(){})
   ```

   

4. **获取路径中的文件名：path.basename()**

   `path.basename()` 方法可以获取路径中的最后一部分，通常用这个方法获取路径中的文件名。

   ```javascript
   path.basename(path[, ext])
   ```

   参数1：必选参数，路径字符串。

   参数2：可选参数，表示文件扩展名。

   加入不传入第二个参数，返回结果是带扩展名的文件名，如 index.html。加入传入第二个的参数如 `'.html'` ，返回结果是不带扩展名的文件名如 index。

   ```javascript
   path.basename(filePath1)              //结果为index.html
   path.basename(filePath1, '.html')            //结果为index
   ```

   

5. **获取路径中的文件扩展名：path.extname()**

   `path.extname()` 方法可以获取路径中的扩展名部分。返回值是以 `.` 开头的扩展名。

   ```javascript
   path.extname(path)
   ```

   

6. 

