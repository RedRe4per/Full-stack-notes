### Appendix 2 项目拆分

1. **创建一个项目**

   先在项目文件夹中创建 src 文件夹，再在其中创建入口文件 index.js，然后运行 `npm init -y` 。

   然后安装 express，dotenv，cors，morgan，Mongoose 包。`npm i express dotenv cors morgan mongoose`。morgan 能显示哪些请求发送到了服务器端。

   

1. **项目拆分（方向一）**

   -- package.json

   -- package-lock.json

   -- src

   ​	|-- index.js 入口文件（server.js，app.js）

   ​	|-- routes

   ​		 |-- tasks.js （task router）（或者命名为 task.routes.js）

   ​		 |-- users.js （user router）（或者命名为 users.routes.js）

   ​		 |-- index.js （把上面所有的router导入进来，再做一个统一的导出）

   ​	|-- controllers （逻辑处理部分）

   ​		 |-- tasks.js （task Controller）（或者命名为 tasks.controllers.js）

   ​		 |-- users.js （user Controller）（或者命名为 users.controllers.js）

   ​	|-- models

   ​		 |-- tasks.js （task Controller）数据库中 task 这个数据的格式设计。用于 ORM（object relational 

   ​																	                                                       mapping，用来跟数据库交互）。

   ​	|-- middleware

   ​		 |-- error-middleware 

   ​		 	 |-- xxxErrorHandler.js

   ​		 |-- authGuard

   ​		 |-- cors

   ​	|-- utils（Helper function，shared function，db）大概率有。

   ​	|-- db

   ​	|-- config 项目配置（环境变量处理），不一定有。

   

   这种拆分方向还有其他的拆分方法，可能把 routes 和 controller 合并，也很常见。上面的拆分方法，routes 里面没有任何逻辑，只是指向了 controllers。

   还有的拆分方法是多一层 services。services 的逻辑是从 controllers 中拆出来的，如果拆的话，controllers 就不负责逻辑处理了。每多加一层项目就更复杂了。

