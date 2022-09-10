进入 StoreSettingPage 后

1. store Information 部分，点击 store information 中的 calendar，进入 store calendar。

2. store calendar 功能演示

   1. **Addtion**: 在 Wednesday 添加 [7:00, 12:00] 营业时间，再添加 [13:30, 17:00] 营业时间。之后在 Monday 添加 [10:00, 16:00] 营业时间。

   2. **Merging**: 在 Wednesday 添加 [12:00, 13:30] 营业时间，**此时三个营业时间合为一体**。

   3. **Delete**: 在 Monday 点击 [10:00, 16:00] 营业时间，切换至删除，点击确认 radio 后删除。

   4. **分段删除**: 在 Wednesday 中点击整块营业时间，切换到删除，输入删除 [12:30, 14:00] 营业时间。**此时营业时间一分为二**。

      

3. 点击back后回到 StoreSettingPage 主页面。添加一个新的店铺。添加后店铺出现在左侧列表中。此时点击 service information 中的 calendar，进入 service weekly calendar。**此处需介绍 service calendar 与 store calendar 的区别与关系**。

4. Sync 功能演示。点击右上 sync 按钮，**此时会将 store 的 calendar 同步过来**；再次点击 sync 按钮，同步会失败并且弹出原因，**这是因为 calendar 不为空或已有被预约过的 service 无法使用 sync，以防覆盖之前数据。**

5. 在此 calendar 中添加 Sunday [20:00, 22:00] 营业时间，返回失败的结果；**此演示说明 service 的服务时间不能超过 store 的 business time**。

6. 点击back，在左侧选择之前准备好的另一个 service。

   1. 在 Wednesday 添加 [7:00, 11:00] 营业时间。此时会添加，并且弹出同步信息。**此处需解释，当用户预约了此服务后，会在数据库中以周为单位产生 bookingRecord 记录。当 service calendar 添加时间时，会为这些已存在的 bookingRecord 同步更新；**
   2. 在 Wednesday 删除 [XX:00, YY:00] （待定）营业时间。此时会删除，并且弹出同步信息。**此处需解释，当 service calendar 删除时间时，会根据各周 bookingRecord 的该时间段是否已被预约来决定是否可以删除。**

   

