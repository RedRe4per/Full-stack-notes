### Put Delete Pagination

1. **状态码问题**

   当请求成功时，nest 会给一个默认的状态码 200。但我们也可以自定义状态码并返回。

   Nest 中不需要记忆所有的状态码，可以用 `@HttpCode(HttpStatus.提示)` 来选择提示的状态，这样就会自动返回相应的状态码。

   ```javascript
   import { Controller, Get, Param, Post, Body } from '@nestjs/common';
   
   @Controller('coffees')   
   export class CoffeesController {
       @Post()
       @HttpCode(HttpStatus.GONE)  //装饰器位置，返回410GONE。
       create(@Body('name') body){   
           return body;
       }
   }
   ```

   `@HttpCode(HttpStatus.提示)` 是放在回调函数之前的，这意味着它后面的回调函数返回的结果必须是唯一确定的状态。

   

2. **@Res() 原生 express 响应处理方法**

   `@Res()` 装饰器可以在端点方法参数中使用，让我们使用原生 express 响应处理方法。

   ```javascript
   @Controller('coffees')   
   export class CoffeesController {
       @Get()
       findAll(@Res() response){
           response.status(200)send('This action returns all coffees');
       }
   }
   ```

   这种方法很灵活，能提供头操作，库特定功能等，但是应该小心使用。它的缺点是失去了依赖于 Nest 标准响应处理的 Nest 功能的兼容性，例如拦截器和 `@HttpCode()` 装饰器。这也会让代码更难测试，并且必须模拟响应对象。

   

3. **Put 和 Patch**

   <font color='red'>Put 会替换掉整个资源，因此我们需要将整个对象包含在请求有效的负载中。</font>

   <font color='red'>Patch 的不同之处在于，它只修改了部分资源。如果我们愿意，甚至可以只更新资源的单个属性。</font>

   Put 和 Patch 对应的方法为 `update` 。

   ```javascript
   @Controller('coffees')   
   export class CoffeesController {
       @Patch(':id')
       update(@Param('id') id: string, @Body() body){   //注意写法
           return `This action updates #${id} coffee`;
       }
   }
   ```

   这里要注意写法。用 Params，Query 或者 req.body 参数就要先声明对应的 @装饰器。此外，如果是全部的 res.body，应该写为 `@Body() body` , `()`不能丢。 

   

4. **Delete**

   Delete 对应的方法为 `remove()` 。

   ```javascript
   @Controller('coffees')   
   export class CoffeesController {
       @Delete(':id')
       remove(@Param('id') id: string){   //remove, 注意也要传入id
           return `This action removes #${id} coffee`;
       }
   }
   ```

   

5. **Pagination**

   我们希望使用路径参数：识别特定资源，在使用查询参数时：过滤或排序该资源。

   Nest 中的 `@Query` 装饰器用于获取所有或特定部分的查询参数。

   ```javascript
   @Controller('coffees')   
   export class CoffeesController {
       @Get()
       findAll(@Query() paginationQuery){
           const { limit, offset} = paginationQuery;
           return `This action returns all coffees. Limit: ${limit}, offset: ${offset}`;
       }
   }
   ```

   
