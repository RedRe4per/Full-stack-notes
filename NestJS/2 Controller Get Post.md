### Controller Get Post

1. **通过运行 Nest CLI 来生成一个控制器**

   命令：`nest generate controller` ，可以简写为 `nest g co`。然后输入 controller 的名字。（如果不想生成测试文件，应该输入 `nest g co --no-spec` ）

   运行后，nest 会帮我们创建好一个文件夹，内含 controller 和 spec 文件。这时 app.module.ts 文件中会自动引入这个 controller 至 controllers 数组中。

   如果想在 src 的子文件夹下创建 controller，命令可以改写成 `nest generate controller modules/abc`。 如果想看模拟输出，可以用 `nest generate controller modules/abc --dry-run`。他不会真正创建文件。

   

2. **URL 访问与 controller 匹配机制**

   Nest 用 <font color='red'>`@Controller('路由')`</font> 来匹配 controller 与 url。

   ```javascript
   @Controller('coffees')    //当以GET访问 http://localhost:3000/coffees时就能访问到。
   export class CoffeesController {}
   ```

   当 controller 为空时，会返回 404 和错误提示。还要注意，<font color='red'>Controller 和 Get/Post 等方法是从 @nestjs/common 中引入的</font>。

   

3. **构建 http 处理程序， Get**

   首先从 @nestjs/common 中引入 Get 等 Methods。Get 对应的方法为 `findAll()` 和 `findOne`。

   ```javascript
   import { Controller, Get } from '@nestjs/common';
   
   @Controller('coffees')   
   export class CoffeesController {
       @Get()
       findAll(){
           return 'This action returns all coffees';
       }
   }
   ```

   

   **嵌套路径**

   在 `@Controller('一级路径')` 修饰的类中，可以嵌套次级路径。

   ```javascript
   @Controller('coffees')   
   export class CoffeesController {
       @Get('flavors')    //此处放二级路由。
       findAll(){
           return 'This action returns all coffees';
       }
   }
   ```

   这时访问 localhost:3000/coffees/flavors，即可访问到内容。 

   

   <font color='red'>**使用路由参数（动态路径）**</font>

   在装饰器中写入 `(':id')` 就可以使用路由参数，并且从 <font color='red'>@nestjs/common 中引入 Param</font>。@Param() 装饰器让我们可以获取所有传入的请求参数，并在方法的函数体内使用它们。

   1. 当 @Param() 装饰器内部不传递任何东西时，它会接收所有请求参数，让我们从对象访问 params.id。

      ```javascript
      import { Controller, Get, Param } from '@nestjs/common';
      
      @Controller('coffees')   
      export class CoffeesController {
          @Get(':id')    //此处放二级路由。
          findOne(@Param() params){
              return `This action returns #${params.id} coffees`;
          }
      }
      ```

      

   2. 当 @Param() 装饰器传入参数时，首先要声明参数类型，然后直接使用参数即可。

      ```typescript
      import { Controller, Get, Param } from '@nestjs/common';
      
      @Controller('coffees')   
      export class CoffeesController {
          @Get(':id')    
          findOne(@Param('id') id: string){   //此处声明参数类型。
              return `This action returns #${id} coffees`;
          }
      }
      ```

      

4. **Post 和 @Body 装饰器**

   @Body装饰器用于获取 request.body 的所有或特定部分。注意 Post 和 Body 都要从 @nestjs/common 中引入。Post 对应的方法为 `create` 。

   ```javascript
   import { Controller, Get, Param, Post, Body } from '@nestjs/common';
   
   @Controller('coffees')   
   export class CoffeesController {
       @Post()    
       create(@Body() body){   
           return body;
       }
   }
   ```

   

   与 @Param 装饰器相同，可以不访问 body 整体，而是特定部分。

   ```javascript
   import { Controller, Get, Param, Post, Body } from '@nestjs/common';
   
   @Controller('coffees')   
   export class CoffeesController {
       @Post()    
       create(@Body('name') body){   //传入参数
           return body;
       }
   }
   ```

   这种方式的问题是，如果只访问特定属性，其他属性不会被验证。

   