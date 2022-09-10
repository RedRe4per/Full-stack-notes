### Service

1. **创建 service**

   创建 service 时，先输入`nest generate service` ，缩写`nest g s`。之后输入名称。

   service 用来处理逻辑，并且抽离出来之后可以复用。在 nest 中，每一个 service 都是一个 provider。

   

2. **Provider**

   <font color='red'>Provider 的主要思想是它可以注入**依赖**。这意味着对象之间可以创建各种关系，并且将对象实例连接在一起的逻辑都可以由 Nest 运行时系统处理，而不是尝试自己创建和管理这种类型的依赖注入。</font>

   Provider 在 nest 中是装饰器名为 `@Injectable()` 的类。

   

3. **Provider 依赖**

   如果想注入提供者，我们可以简单地使用构造函数。

   在 Contoller 文件中，在 Controller 类中写入 `constructor(){}`。

   ```javascript
   import { CoffeesService } from './coffees.service';
   
   @Controller('coffees')   
   export class CoffeesController {
       constructor(private readonly coffeesService: CoffeesService){}
       
       @Post()
       @HttpCode(HttpStatus.GONE)  //装饰器位置，返回410GONE。
       create(@Body('name') body){   
           return body;
       }
   }
   ```

   **private**：typeScript 用法，允许我们在同一位置立刻 declare 和 initialize CoffeesService 成员。并且它只能在类本身内访问，因此是 private。

   **readonly**：确保不会修改引用的服务，只从中访问内容。

   **coffeesService** ：命名参数。

   **: CoffeesService**：在 typeScript 中，用类型来管理依赖。nest 将通过创建 CoffeesService 实例并将其返回给我们的 CoffeesController 来解析 CoffeesService，或者在有已存在的实例时返回该实例。此依赖项已解析并传递给控制器构造函数，或分配给此处指定的属性。

   

4. **Service 逻辑，CRUD**

   在 service 文件中：

   ```javascript
   import { Coffee } from './entities/coffee.entity';   //coffee类，略
   
   @Injectable()
   export class CoffeesService {
       private coffees: Coffee[] = [   //创建数组，使用多个实例。
           {
           	id: 1,
               name: 'Shipwreck Roast',
               brand: 'Buddy Brew',
               flavors: ['chocolate', 'vanilla']
       	}
       ];
   
   	findAll(){return this.coffees};
   	findOne(id: string){item => item.id === +id};
   	create(createCoffeeDto: any){this.coffees.push(createCoffeeDto)};
   	update(id: string, updateCoffeeDto: any){
           const existingCoffee = this.findOne(id);
           if(exsitingCoffee){}
       }
   	remove(id: string){
           const coffeeIndex = this.coffees.findIndex(item => item.id === +id);
           if(coffeeIndex >= 0){ this.coffees.splice(coffeeIndex, 1) };
       }
   }
   ```

   

5. **在 controller 中使用依赖**

   在 controller 文件中：

   ```javascript
   @Controller('coffees')
   export class CoffeesController {
       constructor(private readonly coffeesService: CoffeesService){}
       
       @Get()
       findAll(@query() paginationQuery){
           //const {limit, offset} = paginationQuery;
           return this.coffeesService.findAll();
       }
       
       @Get(':id')
       findOne(@Param('id') id:string){
           return this.coffeesService.findOne(id);
       }
       
       @Post()
       create(@Body() body){
           return this.coffeesService.create(body);
       }
       
       @Patch(':id')
       update(@Param('id') id: string, @Body() body){
           return this.coffeesService.update(id, body);
       }
   
   	@Delete(':id')
   	remove(@Param('id') id: string){
           return this.coffeesService.remove(id);
       }
   }
   ```

   

​	