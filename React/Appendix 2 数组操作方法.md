### 数组操作

1. push 尾部添加

2. pop 尾部取出

3. shift 头部取出？

4. unshift 头部添加？

5. splice 一般用于数组中间删除。虽然有其他功能，但是用多少。

   -------

   遍历

1. for 

2. for of  取的是 arr 中的值，或者 obj 中的 value

   for(let fruit of fruits)

3. for in 取的是 obj 中的 key。

4. forEach 是 arr 类型的方法。第一个参数是接收一个回调函数，第二个参数是index，第三个参数少用。

   forEach 和 for 的区别：for 可以用 break 提前终止循环，但是 forEach 不支持 break。

5. Map 每一项取出便利，加工。Map 是映射的意思。原始数组会和新数组长度一致。

   const newFruits = 

6. **reduce** 接受两个参数 累加用。



----------------------------------

​	搜索

1. indexOf
2. some 看当前数组是否包含想找的对象，包含就返回 true，不包含就返回 false。
3. find 接受一个回调函数，并且监听返回值是否是 true。找到 true 就结束，找到 false 就继续。用来查找数组中的特定项。
4. filter 会把整个数组遍历一遍，找到所有符合要求的元素（并装在新数组中）。

--------

​	其他

1. set 不是方法，而是一个构造函数，可以把添加的数组去重，或者无法新添加新的重复数组。 用于数组去重。

   快速去重：const uniqueArray = [...new Set(Array)]；就是把 array 传给 set 去重后再展开包装成普通数组。

2. 



事件循环 1小时56分

nodeJS 2小时22分