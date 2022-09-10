### 数据传输对象DTO 数据验证

1. **DTO**

   DTO 是 data transfer object 数据传输对象的缩写。DTO 是一个对象，用于封装数据并且将其从一个应用程序发送到另一个应用程序。DTO 帮助我们定义系统内的接口或输入输出。

   即，DTO 定义了要接收数据的格式。类似于 Joi 验证。objectId 这种数据库自动生成的就无需验证。

   DTO 只是简单的对象，它们不包含任何业务逻辑、方法或任何需要测试的东西。

   

2. **生成 DTO 文件**

   生成位置： coffees.controller.ts 同级的 dto 文件夹下。

   -- src

   ​	|-- coffees 模块文件夹

   ​		 |-- coffees.module.ts 帮助我们保持代码的条理性，并为应用程序及其功能建立清晰的边界。

   ​		 |-- coffees.controller.ts 

   ​		 |-- coffees.service.ts 

    		|-- dto

   ​			  |-- create-coffee.dto 

   

   生成方式：使用 nest cli：`nest generate class 路径和名称.dto --no-spec` ，简写为 `nest g class 路径和名称.dto --no-spec` 。例如，`nest g class coffees/dto/create-coffee.dto --no-spec` 。添加 `--no-spec` 是为了避免生成测试文件。

   

3. **DTO 文件**

   /dto/create-coffee.dto 中：

   ```typescript
   export class CreateCoffeeDto {
       name: string;
       brand: string;
       flavors: string[];
   }
   ```

   

4. **在 controller 中使用 DTO**

   coffees.controller.ts 中：

   ```typescript
   @Post()
   create(@Body() createCoffeeDto: CreateCoffeeDto) {
       return this.coffeesService.create(createCoffeeDto); //注意此处创建时要用DTO实例
   }
   ```

   

5. 

