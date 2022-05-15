### ES6 1   let const 解构赋值

1. **let 声明变量a**

   let 是 ES6 中新的变量声明方式，用来代替var。

   ```javascript
   let a;
   let b, c, d;
   let e = 100;
   let f = 521, g = 'iloveyou', h = []; 
   ```
   
   ​	var：允许重复声明，能声明提升，能自动声明。
   
   ​	let：不允许重复声明，没有声明提升。<font color='red'>只在块级作用域内有效。暂时性死区。</font>
   
   
   
   块级作用域：一个{ }就是一个块级作用域。常见的：if，for，和函数中。
   
   ​	注意：
   
   1. {{}} 这种嵌套的块级作用域，在外层{}中的 let 声明的变量，在内层 {{}} 中也有效。这是因为内层{{}}也是外层{}块级作用域的一部分。（全局变量在局部作用域也有效）
   
   2. for循环中，let 虽然写在了{}外面，如 `for(let a=0; a<n; a++){}` ，但是由于for循环内部处理，let声明的元素实际是在后面的{ }块级作用域中定义的。并且，每循环一次，便生成了一个新的 let a(新值)，也生成了一个新的{ }块级作用域。因此，<font color="RED">for循环几次就有几个{ }块级作用域</font>。
   
   ​	例1：var
   
   ```javascript
   var a=[];
   for(var i=0; i<10; i++){
       a[i] = function(){
           console.log(i)
       };
   }
   a[6]()//输出为10。这是因为var a是全局变量，每次运行i都会增加，最后加到10，即输出10（同this那一节课）
   ```
   
   ​	例2：let
   
   ```javascript
   var a=[];
   for(let i=0; i<10; i++){
       a[i] = function(){
           console.log(i)
       };
   }
   a[6]()//输出为10。因为let生成了10个{}块级作用域，每个let声明的i都只在它的块级作用域内有效（而非全局）
   ```
   
   
   
   暂时性死区：<font color="red">let声明的变量自动绑定当前块级作用域。即在一个块级作用域内如果有let声明变量，在这个块</font><font color="red">级作用域内只能用它，外部的同名变量不能使用。</font>例：
   
   ```javascript
   var tmp = 123;
   if(true){
   	tmp = 'abc';
       let tmp;
   }//输出为报错。因为tmp没有声明。
   ```

​			

2. **const 声明常量**

   const 声明的常量不能修改，用来防止常量被意外更改。

   const 声明的时候必须赋初始值。

   const 的常量一般使用大写（潜规则）。

   const 可以用于：正则表达式，用户名/密码，DOM操作时 document.getElementBy...的元素等。还有一种代码风格是只要不确定的一律用 const。

   对于数组和对象的元素修改，不算做对常量的修改，不会报错。因为常量的地址没变。

   ```javascript
   const TEAM = ['Ali','Neil','Tom','Tony'];
   TEAM.push('Ben'); //正确语法
   TEAM = 100; //报错
   ```

   

3. **数组的解构赋值**

   解构赋值可以用来声明多个变量。语法为：

   ```javascript
   let [a, b, c] = [1, 2, 3] //等同于 let a=1; let b=2; let c=3;
   ```

   即let左边为变量的数组，右边为数据的数组，两边结构要相同。

   注意：

   1. 如果let两边的变量和数据数量不匹配，就从左到右能匹配的一一匹配。解构失败的变量为undefined。

   2. 逗号可以占位。

      ```javascript
      let [ , , a] = [1, 2, 3] //a=3
      ```

   3. 解构赋值中出现嵌套的情况，只要两边嵌套结构相同就可以成功匹配。

   4. 解构赋值可以用于两个变量交换数据，如：

      ```javascript
      [x, y] = [y, x]
      ```

   

4. **对象的解构赋值**

   ```javascript
   const stu1 = {
       name:'tom';
       age:18;
       ability: function(){
           console.log("I can eat");
       }
   }
   let {name, age, ability} = stu1;
   ```

   

   连续解构赋值

   ```javascript
   const {keyWordElement:{value}} = this	//可以获得this.keyWordElement.value值，即多重属性
   ```

   多重属性可以用连续解构赋值，但是注意这里的中间属性 keyWordElement 没有被定义。

   

   解构赋值并重命名

   ```javascript
   let obj = {a:{b:1}};
   const {a:{b:data}} = obj;	//旧名字：新名字
   ```

   ```javascript
   const {keyWordElement:{value:keyWord}} = this	//有些有经验的程序员会这么写
   ```

   

4. **字符串的扩展：模板字符串**

   **``**中写字符串，允许换行。**${ }**中写变量，不用拼接。

   

6. **对象的简化写法**

   <font color='red'>ES6 允许再大括号里面，直接写入变量和函数，作为对象的属性和方法</font>

   ```javascript
   let name = 'Web age';
   let change = function(){
       console.log('I can change you');
   }
   
   const school = {
       name, //等同于 name: name
       change, //等同于 change: change
       improve(){ //等同于 improve: function(){}
           console.log('I can improve your skills');
       }
   }
   ```

   

