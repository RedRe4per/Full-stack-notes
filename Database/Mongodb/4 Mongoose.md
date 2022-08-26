### Mongodb 4 Mongoose

1. **Mongoose 介绍**

   Mongoose 是一个包，它使用 promise 和 async / await。Mongoose 是一个 ORM（object relational mapper）或 ODM（object data mapping），它专门针对 Mongodb。它针对 CRUD 等功能进行了封装，提供了新的接口，更便利。

   其他数据库也有类似的包，如 sequelize 包针对 mySQL 等数据库。实际开发中很少会直接和数据库交互，都是用 ORM 库来 CRUD。如果追求效率极致，可能会手写 ORM 库，因为流行的 ORM 库是针对大部分用户。

   

   数据从数据库取到服务器，中间会经过 Mongoose 这层。Mongoose 会把 json 原始数据转换成 JS 中的 Object，从而我们可以通过对 Object 操作的方式来操作 Mongoose 的对象。这里会损失一些性能，而有时不需要转换，就需要自己优化。

   

2. **Mongoose 中的关键字**

   schema，Model，document 是 Mongoose 中的关键字。

   + schema 是数据设计图，列出数据的字段等。

   + Model （对应 Mongodb 中 collection）是通过 schema 的图纸，建立一个模型。一个用处是用来生成 document（创建 model 实例），需要传入 schema 中定义的字段。

     Model 的另外一个用处是对数据的 collection 操作，可以添加 document，搜索整个 collection 等。

   + document 和 Mongodb 中的 document 稍有不同，它类似于 Mongodb 中的 document。它是一个 JS 对象，并且是由 Mongoose 创建的。因此，它不仅是数据库中 bson 格式数据，它同时支持 Mongoose 中的 API，更方便地处理数据。

   ```javascript
   const schema = new mongoose.Schema({name: String});
   const Model = mongoose.model('Model', schema);
   const document = new Model({name: 'document'})
   ```

   

   [Mongoose 中的运算符](https://www.mongodb.com/docs/manual/reference/operator/)

   

3. **安装 Mongoose**

   `npm i mongoose`

   因为 Mongoose 是用来创建某一资源的模型，所以应放在 src 下的 models 文件夹中。

   

4. **数据库中图片的处理**

   数据库不会直接存储数据，而是先要将图片上传至特定平台中，平台返回 url 后再存储至数据库。

   

5. **建立 model**

   

6. 