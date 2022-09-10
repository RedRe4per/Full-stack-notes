### ES6 2  箭头函数 rest

1. **函数的扩展：箭头函数 =>**

   ```javascript
   let fn = function(m){return m}; //普通函数
   let fn = (m) => {return m} //箭头函数完整写法
   let fn = m => m //简写后的箭头函数
   ```

   箭头函数写法

   ​	箭头函数的完整写法：只把普通函数中参数 (m) 前的 function 改为参数后的 =>。（代码第一行与第二行）

   ​	箭头函数只有函数字面量的声明方式，没有 function fn( ){ }; 的声明方式。

   ​	箭头函数简写

   ​			1. 如果箭头函数的参数只有一个，可以省略 ()。没有参数的话 () 不能省略。

   ​			2. 箭头函数中如果想直接 return 返回一个表达式（数据），可以把 {return } 直接省略。注意必须是

   ​				return + { } 一起省略。省略 {return } 一般用于函数不进行运算而只想返回一个值。如果 { } 中还要

   ​				进行别的操作（如条件判断）就不要省。

   ```javascript
   	//正确的写法	
   	let fn = m => m;
   	let fn = m => 100;
   	let fn = m => m + 5;
   	//错误的写法
   	let fn = m => {m + 5}; 
   ```

   ​			3. 如果想返回一个对象 { }，会有歧义，因为程序解析不知道是对象 { } 还是函数体 { }。

   ​				因此，直接返回一个对象时需要外面加一个 ( )，如 

   ```javascript
   	let fn = () => ({name:'Tom'})
   ```

   ​					

   箭头函数特性

    1. this 指向是静态的，this始终指向函数声明时所在作用域下的 this 的值。

       普通函数的 this 指向函数调用时所在的对象。例：

       ```javascript
       var x = 100;
       var obj = {
           x:10
           getX: function(){
               console.log(this.x)
           }
       }
       obj.getX() //10 obj调用的函数，this指向obj
       a = obj.get;
       a(); //100 window调用的函数，this指向window
       ```

       箭头函数中 this 指向函数定义时所在的对象，不会因为调用者的变化而改变。

       ```javascript
       var x = 100;
       var obj = {
           x:10
           getX = () => {
               console.log(this.x)
           }
       }
       obj.getX() //10 this指向obj
       a = obj.get;
       a(); //10 this指向obj
       ```

   

   2. 箭头函数不能作为构造实例化对象

      ```javascript
      let Person = (name, age) => {
          this.name = name;
          this.age = age;
      }
      let me = new Person ('Tom', 30);
      console.log(me) //报错
      ```

      

   3. 不能使用 arguments 变量

      ```javascript
      let fn = () => {
          console.log(arguments);
      }
      fn(1, 2, 3); //报错。ReferenceError：arguments is not defined
      ```

      

2. **箭头函数概念案例**

   ```javascript
   function Timer(){
       this.s1 = 0;
       this.s2 = 0;
       //箭头函数
       setInterval(() => this.s1++, 1000); 
       //普通函数
       setInterval(function(){
           this.s2++;
       }, 1000)
   }
   var timer = new Timer()
   setTimeout(() => console.log('s1: ', timer.s1), 3100); //3
   setTimeout(() => console.log('s2: ', timer.s2), 3100); //0
   ```

   在 `timer = new Timer()` 时，Timer 中的代码全部被执行，包括定时器部分。注意这里定时器是直接执行了而不是绑定给了 Timer。

   易错的地方是，定时器是 window 对象的方法，而不是 timer 对象的。因此，在 `timer = new Timer()` 时定时器是被 timer 对象创建的（因为构造函数 Timer 中的代码在 Timer 被调用之前不会执行）。这就导致了当使用箭头函数的时候，箭头函数中的 this 指向是函数的创建者 timer；而定时器的调用者是 window。因此非箭头函数的情况下，定时器中的 this 会指向定时器的调用者 window。

   

   ```javascript
   var fn = () => {console.log(this)};
   fn()
   ```

   此例中箭头函数的创建者和调用者都是 window。



3. **rest 参数**

   用来代替原生 JS 中的 arguments 参数。rest 参数可以取到<font color='red'>余下</font>的所有实参。

   arguments：结果是一个对象。

   ```javascript
   function data(){
       console.log(arguments);
   }
   data('a', 'b', 'c');
   ```

   ![image-20220218220528434](C:\Users\GUOQING ZHU\AppData\Roaming\Typora\typora-user-images\image-20220218220528434.png)

   rest：<font color='red'>结果是一个数组</font>

   rest 声明方式为 ...args。

   ```javascript
   function data(...args){
       console.log(args);
   }
   data('a', 'b', 'c');
   ```

   ![image-20220218221349900](C:\Users\GUOQING ZHU\AppData\Roaming\Typora\typora-user-images\image-20220218221349900.png)

   因此 rest 参数就可以使用数组的方法，如 filter，some，every，map，提高了灵活度。

   rest 参数必须放到参数最后。

   ```javascript
   function fn(a, b, ...args){
       console.log(a); //结果为1
       console.log(b); //结果为2
       console.log(args); //结果为 3， 4， 5， 6
   }
   fn(1, 2, 3, 4, 5, 6);
   
   //如果...args往前放
   function fn(a, ...args, b){
       console.log(a); 
       console.log(b); 
       console.log(args); 
   }
   fn(1, 2, 3, 4, 5, 6); //结果报错
   ```

   

3. 

4. +-+*函数的默认参数**

   ```jsx
   function sum(a = 1, b = 1) {
       return a + b
   }
   sum()
   ```

   当传入参数数量不够时，或传入 undefined 时，用默认参数值代替。
