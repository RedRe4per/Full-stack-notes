### P3 Major bug

1. **后端 user.save() 失效**

   已知问题：在发送任何请求时，如果后端处理函数包含 `user.save()` ，并且此 user 没有 user.password，（老 schema 中的 user）会返回错误：

   ```
   <pre>ValidationError: User validation failed: password: Path `password` is required.<br> &nbsp; &nbsp;at model.Document.invalidate (C:\Users\USERNAME \Documents\GitHub\BookingLet\back_end\node_modules\mongoose\lib\document.js:2970:32) &nbsp; &nbsp;at C:\Users\USERNAME \Documents\GitHub\BookingLet\back_end\node_modules\mongoose\lib\schematype.js:1333:9<br> &nbsp; &nbsp;at processTicksAndRejections (node:internal/process/task_queues:78:11)</pre>
   ```

   

   造成后果：部分涉及 `user.save()` 的 API （如 addStoreById,  addOrder）在 userId 不存在 user.password 词条时，无法正确返回 res.json() 结果。调用这些 API 时可以正确创建 store/order，但是 user-store/order 的关联无法创建，因此 user.stores 和 user.orders 中无法找到刚刚创建的 ObjectId。

   此 bug 对于存在 user.password 词条的 userId 并不会出现。

   建议修改方案：在数据空的 user table 中，更新所有没有 password 词条的 user document。<font color='red'>（请勿直接删除这些 user，因为这些 user 关联着几乎所有 store 和 order，删除后产生重大不可修复的 bug。）</font>

   

2. **Login/Logout bug **

   Application - Local Storage - Key 中 user 和 loggedIn 的 value 一直是错的。

   user 的错误 value 有 'null', '[object Object]'; loggedIn 的 true/false 状态一直是混乱的。

   

   造成后果：npm start 后有概率白屏，addIcon bug。

   

   暂时解决方案：我们在 const AddIcon = ({ favoriteUsers }) => {} 中使用：

   ```javascript
   if (user === '[object Object]' || user === 'null') {user = '';}
   ```

   捕获并包裹住了错误。这样即使在 Application - Local Storage - Key 中 user value 一直错误，也不会白屏。

   

   但是此方案没有根本解决问题，也没有解决 loggedIn 的 value 错误的问题。请尽快修复。