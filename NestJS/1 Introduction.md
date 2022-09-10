### Introduction

1. **NestJS 与 NodeJS 区别**

   NestJS 是一个框架，让程序员专注于手头的应用程序问题，而非诸如设置 TypeScript，API 路由，错误处理，中间件设置等微小实现细节。

   将 NestJS 视为 NodeJS 本身之上的一个层，抽象出困难的任务，工具和样板代码，并且为应用程序开发添加了一个完整的工具包。NestJS 默认用 express 作为底层，也可以选用 Fastify 或者其他（但要设置兼容库）。

   

2. **使用 NestJS 之前**

   首先要安装 NodeJS，版本至少 12 或 13。在 Terminal 中查看：`node --version`。

   安装 cli: `npm i -g @nestjs/cli`。

   安装后查看 nest 版本号: `nest --version`。

   

3. **Nest cli**

   nest cli 是 nestJS 的配套工具，可以帮我们生成文件运行编译甚至捆绑我们的应用程序。它包含很多 commands，可以用 `nest --help` 来查看。

   

4. **创建第一个 nest 应用程序**

   在 Terminal 中，输入 `nest new`。之后根据提示，选择名字和包管理器。创建之后，输入 `cd 新文件名`， `npm run start`，就可以打开浏览至 localhost: 3000 来打开文件。

   

5. **Nest 文件夹结构**

   在 Nest 应用程序内部，所有东西都有一个定义好的结构。在文件夹中，有很多之前熟悉的文件，但是要注意一个名为 <font color='red'>Nest cli json</font> 的特定独有文件。

   nest 的入口文件时 src 下的 main.ts 文件。nest 文件是通过 NestFactory.create(AppModule) 来创建的。<font color='red'>AppModule 是我们应用程序的根模块</font>，包含了我们应用程序运行所需的一切。它包含很多小的模块，组合后就是完整的应用程序。

   打开 app.module.ts 文件后，可以看到装饰器 @Module()。装饰器可以用于类或其他方法。@Module({ }) 中的第一层是入口级文件 app.modules.js 的 controllers 和 providers，如果没有就删掉。之后，`import: []` 是用来加载其他模块用的。这些模块的文件夹放在 src 目录下。

   

6. **controller and Service basic**

   Controller 是一个类，但是有 @Controller() 修饰器。Controller 用来处理特定请求。Controller 中需要用到 service 把逻辑分离出来。

   在 app.controller.ts 文件中：

   ```javascript
   @Controller()
   export class AppController{
       contructor(private readonly appService: AppService){}
       
       @Get()
       getHello(): string{
           return this.appService.getHello();
       }
   }
   ```

   在 app.service.ts 文件中：

   ```javascript
   @Injectable()
   exports class AppService {
       getHello(): string{
           return 'Hello World!';
       }
   }
   ```

   

7. **发送请求测试的软件**

   Insomnia & Postman

   

8. **在开发模式下启动 Nest**

   `npm run start: dev`。这个模式集成了 nodemon 功能。