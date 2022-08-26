### Mongodb 2 库 数据 命令行CRUD

1. **Mongodb 结构**

   1. Databases Server：安装 mongodb 之后，启动的 mongodb 程序时，启动的就是 databases server。 

   2. Databases：databases server 中有多个 database。

   3. Collections：每个 database 中有多个 collection。如学校系统中，老师和学生是不同 collection。

   4. Documents：每个 collection 中有多个 document，类似 json （即对象）的格式。例如 `{_id: ObjectId('xxx1'), name: 'Tom', grade: 9}` 就是一个 document。

   5. Fields：Document 的类似 json 格式文件中，每一个 key 就是一个 field。

      ![image-20220528151626903](C:\Users\GUOQING ZHU\AppData\Roaming\Typora\typora-user-images\image-20220528151626903.png)

   

   有多种 clients 可以访问数据库

   1. mongo shell：命令行程序

   2. mongodb compass：图形化界面，所有操作通过点击实现，类似 github 桌面版。

   3. script：代码，如 JS

      

2. **数据类型**

   数据类型类似于 JS。常见数据如：

   **_id**: int32 (默认为为 ObjectId，包含一些随机数和机器物理信息，保证不重复)

   <font color='lightgrey'>Name:</font> **Text** (string)

   <font color='lightgrey'>Hobbies: </font>**array** (array of string)

   <font color='lightgrey'>Address: </font>**object** (embeded document)

   <font color='lightgrey'>Wishes: </font>**array** (array of documents)

   **Boolean**

   **Number** (可细分为 int32 (默认)，int64，float)

   **Date** (ISODate (默认), timestamp)

   

3. **Mongodb 命令行基本操作，增删改查**

   1. `show dbs` ：显示数据库信息，database server 中的 databases。默认 admin、config 和 local。

   2. `show collections` ：显示当前数据库中所有 collection 名。

   3. `use 数据库名` ：新建 database（数据库名不存在时），或切换到某个 database（数据库名存在时）。

   4. <font color='blue'>添加单个新的 collection 和 documents</font>（增）：

      ```powershell
      db.集合名.insertOne()
      ```

      db 对象指代当前使用的 database，如 school 数据库。集合名是创建新的集合 collection（集合名不存在时），或使用数据库中已存在的集合 collection（集合名存在时）。`insertOne()` 是添加 document ，参数是 document（对象，即 json）。如：

      ```powershell
      db.students.insertOne({"name":"mason"})
      ```

      返回日志信息：

      ```powershell
      {
              "acknowledged" : true,       #表示服务器收到了请求
              "insertedId" : ObjectId("6291fd3083ebd0086fc7152a")  #Mongodb自动创建ID
      }
      ```

      

      <font color='blue'>一次也可添加多个 documents，即传一个数组，数组中多个 document</font>：

      ```powershell
      db.students.insertOne([{"name":"Raymond"},{"name":"Siri"}])
      ```

      会生成多个 _id 对应多个 documents。

      

   5. <font color='blue'>查找当前 collection 中数据（查找多个）</font>（查），并返回结果

      ```powershell
      db.集合名.find()   #如db.students.find()
      ```

      ```powershell
      { "_id" : ObjectId("6291fe3f83ebd0086fc7152b"), "name" : "Derek" }  #返回结果
      ```

      <font color='blue'>查找当前 collection 中数据（查找一个，并且是当前 collection 中的第一个数据）</font>

      ```powershell
      db.集合名.findOne() 
      ```

      <font color='blue'>查找指定条件数据，条件为某个字段的值为 xxx。</font><font color='red'>注意这里的 key 没有 `" "` 。</font>

      ```powershell
      db.集合名.findOne({name:"max"}) 
      ```

      

      <font color='blue'>`find()` 实际上还有第二个参数，为展示条件（返回结果展示哪些 fileds）。</font>展示条件中想要展示的 field 值为1，默认为0。但是 _id 默认为展示，即值为1。

      ```powershell
      db.students.find({}, {name:1, _id:0})
      ```

      

   6. <font color='blue'>更新数据（改单个）</font>（改）。接收两个参数，参数1为如何筛选数据（找到第一个匹配的 document），参数2为把查找到的 documents 更新成什么样。更新的时候要用到操作符 operator，更新中叫做 update operator：<font color='red'>`$set:{}` </font>。

      ```powershell
      db.集合名.updateOne({name:"Derek"},{$set:{"name":"James"}})
      ```

      也可以添加新的 field：

      ```powershell
      db.集合名.updateOne({name:"James"},{$set:{"Hobbies":["football","gaming"]}})
      ```

      <font color='blue'>更新数据（改多个）</font>，匹配所有符合条件的 documents。

      ```powershell
      db.集合名.updateMany({name:"James"},{$set:{"Hobbies":["football","gaming"]}})
      ```

      

      <font color='blue'>还有一个 `db.集合名.replaceOne()` 方法可以做完整替换。</font>

      

   7. <font color='blue'>删除一个 document</font>。先做筛选，然后删除目标文档。语法同查找，<font color='red'>即 key 没有 `" "` 。</font>

      ```powershell
      db.集合名.deleteOne()
      ```

      ```powershell
      db.students.deleteOne({name:"Derek"})
      ```

      <font color='blue'>删除多个 documents</font>。<font color='red'>注意，`deleteMany({})` 操作时非常危险的，意味着所有的 documents 都能匹配，会删除当前 collection 中所有 documents。</font>开发时候不会用这种命令。

      ```powershell
      db.集合名.deleteMany()
      ```

      

      注意如果删除了当前 collection 中所有 documents，collection 依然存在；想删除当前 collection，命令是 `db.collection名.drop()` 。包括索引等信息也都会被删除。

      

4. **Mongodb 命令行相关的小技巧**

   1. tab 键可填充 collection 名，即只写一个 collection 名开头就行。逻辑同 Node.js 路径。

   2. 如果插入 document 中数据括号缺失（某个括号没关上），返回结果会是 `...` 。解决办法是括号输入时就把开和闭都键入，再回退输入内容。

   3. 也可以传入空的 document：`{}` 。依然是唯一的，因为有 _id。

   4. 添加 document 时也可以指定 _id，如：

      ```powershell
      db.students.insertOne({"_id":"6291fe3f83ebd0086fc7152b","name":"mason"})
      ```

      这是可以正常运行的。但是比起自动生成的 id，指定的 _id 没有 `ObjectId()` 包裹，<font color='red'>意味着类型不一样。自己指定的 _id 是 string 类型，而自动生成的 _id 是 ObjectId 类型。</font>开发时会有第三方 package 帮我们类型转换，因此不用关心。

   

5. **操作符 operator**

   <font color='red'>operator 会以 `$` 开头。</font>[官方详细文档](https://www.mongodb.com/docs/manual/reference/operator/query/)

   1. update operator 更新操作符。 $set
   2. query operator 查询操作符。 $exists，语法为 { field: { $exists: <boolean> } } 。当 boolean 为 true, $exists 匹配包含字段的文档，包括字段值为 null 的文档；当 boolean 为 false, $exists 返回不包含对应字段的文档。
   3. projection operator 展示操作符（取数据用）

6. 