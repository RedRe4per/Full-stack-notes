### ES6 4   Promise（基础）

1. **Promise：ES6中引入的异步编程新解决方案。**

   Promise 主要是解决之前回调地狱的问题。Promise 是一个构造函数，<font color='red'>用来封装异步操作</font>并可以获取其成功或者失败的结果。

   Promise 接收一个函数参数，这个函数参数有两个形参，第一个为成功（默认叫 resolve），第二个为失败（默认叫 reject）。<font color='red'>当调用 resolve( ) 时 Promise 走成功路径，调用 reject( ) 走失败路径。</font>

   ```javascript
   //实例化Promise对象
   const p = new Promise(function(resolve, reject){ //resolve & reject 只是潜规则，可任意命名
       setTimeout(function(){
           let data = 'obj in database';
           if(Math.random()>0.5){
               resolve(data); //自定义的'成功'
           }else{
               reject(data); //自定义的'失败'
           }
       }, 1000);
   }); 
   ```

   

   <font color='red'>成功或失败</font>后就可以调用 Promise 对象的 then( ) 方法。then( ) 方法接收两个函数类型的参数，两个函数参数都有形参，其中成功的形参一般叫 value，失败的形参一般叫 reason。
   
   ```javascript
   p.then(function(value){}, function(reason){})
   ```

   1. <font color='green'>Promise 状态为成功时</font>，就调用 then( ) 中的第一个函数参数。<font color='red'>其中 value 值为之前 resolve( ) 的参数</font>。
   
      ```javascript
      p.then(function(value){
          console.log(value) //value值是之前Promise中resolve()传入的参数
      }, function(reason){})
      ```

   2. <font color='green'>Promise 状态为失败时</font>，就调用 then( ) 中的第二个函数参数。<font color='red'>其中 reason 值为之前 reject( ) 的参数</font>。
   
      ```javascript
      p.then(function(value){ 
      },function(reason){
          console.log(reason) //reason值是之前Promise中reject()传入的参数。
      })
      ```
   
      
   
1. **Promise 封装 Ajax 请求示例。**

   ES5中 JS 的 Ajax请求

   ```javascript
   const xhr = new XMLHttpRequest(); //第一步：创建对象
   xhr.open("GET","http://api.apiopen.top/getJoke"); //第二部：初始化
   xhr.send(); //第三步：发送
   xhr.onreadystatechange = function(){ //第四步：绑定事件，处理响应结果
       if(xhr.readyState === 4){
           if(xhr.status >= 200 && xhr.status < 300){
               console.log(xhr.response); //处理成功的结果
           }else{
               console.error(xhr.status); //处理失败的结果
           }
       }
   }
   ```
   
   使用 Promise 方式对 Ajax 封装
   
   ```javascript
   const p = new Promise((resolve, reject) => {
       const xhr = new XMLHttpRequest(); 
       xhr.open("GET","http://api.apiopen.top/getJoke"); 
       xhr.send(); 
       xhr.onreadystatechange = function(){ 
           if(xhr.readyState === 4){
               if(xhr.status >= 200 && xhr.status < 300){
                   resolve(xhr.response); //先声明成功，并传参至then()再处理 
               }else{
                   reject(xhr.status); //先声明失败，并传参至then()再处理 
               }
           }
       }
   })
   
   //指定成功/失败的回调
   p.then(function(value){
       console.log(value) //成功就传入resolve()的参数xhr.response作为形参value的实参。
   },function(reason){
       console.err(reason) //失败就传入reject()的参数xhr.status作为形参reason的实参。
   })
   ```
   
   此例说明，Promise对于异步成功/失败的结果，处理方式与ES5中不同。原来ES5是在回调函数中操作，现在是在异步任务后面通过 then( ) 方法来指定回调。这样结构清晰，并且不会产生回调地狱的问题。
   
   

3. **<font color='blue'>then( ) 方法</font>**

   Promise 实例具有 then( ) 方法，即 then( ) 方法是定义在原型对象 Promise.prototype 上的。 参数2为可选。then( ) 的返回结果也是一个 Promise 对象。

   ```javascript
   const p = new Promise((resolve, reject) => {
       setTimeout(() => {
           reject('ERROR!')
       }, 1000)
   })
   
   const result = p.then(value => {
       console.log(value)
   }, reason => {
       console.warn(reason)
   })
   
   console.log(result); //结果是一个Promise对象，并且结果是resolved/fulfilled（新版）
   ```

   

   then( ) 方法的返回结果 Promise 对象的状态，由回调函数的执行结果来决定。

   1. <font color='green'>如果回调函数中返回的结果是非 promise 类型的数据，</font><font color='red'>状态为成功，返回值为对象的成功的值。</font>

      ```javascript
      const result = p.then(value => {
          console.log(value)
          return 'success!';
      }, reason => {
          console.warn(reason)
      })
      
      console.log(result); //结果的状态为'resolved'，value为'success!'。
      ```

      <font color='red'>当不写 return 的时候，函数内部默认的返回结果是 undefined。undefined不是Promise类型对象，因此返回状态结果也是成功。</font>

      ```javascript
      const result = p.then(value => {
          console.log(value)
          //return 'success!';   不写return
      }, reason => {
          console.warn(reason)
      })
      
      console.log(result); //结果的状态为'resolved'，value为undefined。
      ```

      

   2. <font color='green'>如果回调函数中返回的结果是 promise 对象，</font><font color='red'>内部 promise 对象返回的状态就决定 then( ) 方法返回的 promise 的状态，并且内部 promise 的值就是 then( ) 方法返回 promise 的值。</font>

      ```javascript
      const result = p.then(value => {
          console.log(value)
          return new Promise((resolve, reject) => { //此promise的返回状态决定了then()方法返回
              resolve('ok');						  //的promise的状态。
          })
      }, reason => {
          console.warn(reason)
      })
      
      console.log(result); //结果的状态为'resolved'，value为'ok'。
      ```

      ```javascript
      const result = p.then(value => {
          console.log(value)
          return new Promise((resolve, reject) => { //失败，同理
              reject('error');	
      }, reason => {
          console.warn(reason)
      })
      
      console.log(result); //结果的状态为'rejected'，value为error。
      ```

      

   3. <font color='green'>如果抛出错误，</font> then( )返回的 promise 状态是 'rejected'，value为抛出的错误值。注意 `throw new Error('test');` 和 `reject(new Error('test'));` 是等价的。

      ```javascript
      const result = p.then(value => {
          console.log(value)
          throw new Error('Error diagnosis')	//抛出错误，有throw即可，如throw 'ERROR';也行。				 
          })
      }, reason => {
          console.warn(reason)
      })
      
      console.log(result); //结果的状态为'rejected'，value为'Error diagnosis'。
      ```

 	

4. **then( ) 方法的链式调用，且可省略 reason 参数**

   ```javascript
   p.then(value => {
   }).then(value => {
   }).then(value => {
   })
   ```

   通过链式调用可以避免回调地狱。

   

   <font color='red'>链式调用实例</font>：每次调用传进新数据，并且保存链上的所有数据。

   ```javascript
   const p = new Promise((resolve, reject) => {    //链上第一个promise
       fs.readFile("./resources/file1.md", (err, data) => {    //node.js语法
           resolve(data);
       });
   });
   
   p.then(value => {    //链上第二个promise
       return new Promise((resolve, reject) => {
           fs.readFile("./resources/file2.md", (err, data) => {
               resolve([value, data]);  //value为file1的data，data为file2的data。
           });
       });
   }).then(value => {    //链上第三个promise。注意此处value是链上第二个promise的resolve值:
       				  //[value，data]，也就是file1和file2的data。
       return new Promise((resolve, reject) => {  
           fs.readFile("./resources/file3.md", (err, data) => {
               value.push(data);
               resolve(value);
            });
       });
   }).then(value => {		//value值就是前三个文件的内容（的数组）
       console.log(value.join('\r\n'));   //拼接  
   })
   ```

   

   <font color='blue'>中断 Promise 链</font>

   在没有 catch( ) 的 promise 链，每个链上的 then( ) 都有成功和失败两个函数参数。但要注意，无论是成功还是失败（return非Promise，return成功的Promise，抛出错误），都会触发下一个链上的 then( )。

   如果想在链中某个 then( ) 触发失败后直接结束链式调用，要在这个 then( ) 的失败函数中调用一个<font color='red'>初始化状态的Promise 实例。</font>

   ```javascript
   return new Promise(() => {});
   ```

   

5. **catch( )**

   Promise.prototype.catch( ) 是 .then(null, rejection) 的语法糖，catch( ) 方法用于指定 Promise 失败的回调，可以统一处理 Promise 链上的错误。即使用 catch( ) 的话链上的所有 then( ) 都不用写失败回调了。

   ```javascript
   const p = new Promise((resolve, reject) => {    
       setTimeout(() => {
           reject("Error!");
       }, 1000)
   });
   ```

   ```javascript
   p.then(function(value){}, function(reason){   //方法一：通过then()来指定失败的回调
       console.error(reason)
   })
   ```

   ```javascript
   p.catch(function(reason){    //方法二：通过catch()来指定失败回调。用写then()的第一个value参数。
       console.error(reason)
   })
   ```



[Promise详细教程](https://www.bilibili.com/video/BV1GA411x7z1?from=search&seid=3434525656507584414&spm_id_from=333.337.0.0)





