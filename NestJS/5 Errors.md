### Errors

1. **Nest 中错误的选择**

   1. 抛出异常
   2. 使用库特定的响应对象
   3. 创建拦截器，利用异常过滤器

   此外，nest 还具有用于所有常见错误响应的辅助方法，包括帮助类。

   

2. **抛出异常**

   在 service 文件中：

   ```typescript
   findOne(id: string){
       const coffee = this.coffees.find(item => item.id === +id);
       if(!coffee){
           throw new HttpException(`Coffee #${id} not found`, HttpStatus.NOT_FOUND);
       }
       return coffee;
   }
   ```

   

3. **帮助类**

   包括 NotFoundException，InternalServiceErrorException，BadRequestException 等。

   ```typescript
   findOne(id: string){
       const coffee = this.coffees.find(item => item.id === +id);
       if(!coffee){
           throw new NotFoundException(`Coffee #${id} not found`);  //此处替换掉，但返回相同
       }
       return coffee;
   }
   ```

   

4. **Nest 内置的异常层自动捕获异常**

   类似于 express-error 自动处理包。

5. 