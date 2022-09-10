### customer booking page

1. 页面挂载之后，首先调用 getAllInfos() 这个API。其中在 req.body 中传入 storeId 的参数。此时会返回一个 serviceInfo 数组，它们都是页面商店下关联的 serviceInfo。数组长度一般为 1-10。

2. serviceInfo 对象数组中，每个 serviceInfo 有 maxPersonPerSection 属性(number)。前端应遍历 serviceInfo 对象数组，并且取出对象数组中 serviceInfo.maxPersonPerSection 的最大值。

   在 Numer of people 的下拉菜单中，选项为 1 - 最大值。

3. 