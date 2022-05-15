### CSS 技巧2

1. **background-color 和 background**

   background 可以不设置为 color，而是设置成渐变色。

   

2. **阴影效果**

   用 box-shadow。它的第一个值是 x 的偏转轴，第二个值是 y 的偏转轴， 第三个值是模糊处理程度（越高阴影越模糊，0-100），第四个值是颜色，可以使用 rgba。例如：

   ```css
   box-shadow: 25px 25px 75px rgba(0,0,0,0.25);
   ```

   注意这个效果是 x 轴和 y 轴的单侧阴影，同时只能兼顾两个边。四个边应该用两层 box-shadow。

   

   如果觉得一层阴影太单薄，也可以加多层阴影。不用另写一个 box-shadow，而是 rgba 后面改逗号，续写下一层阴影。

   ```css
   box-shadow: 25px 25px 1px rgba(0,0,0,0.25), 10px 10px 70px rgba(0,0,0,0.25);
   ```

   

   内置阴影属性：inset。其第一个第二个值可为负（左上边为正，下右边为负）。它会在元素边界内产生阴影。内置阴影的用途是配合外置阴影做出<font color='red'>凹凸效果</font>。

   ```css
   box-shadow:inset -5px -5px 15px rgba(0,0,0,1);
   ```

   ```css
   box-shadow: 25px 25px 1px rgba(0,0,0,0.25), 
   			10px 10px 70px rgba(0,0,0,0.25),
   			inset -5px -5px 15px rgba(0,0,0,1),
   			inset 5px 5px 15px rgba(0,0,0,0.5);   //内外阴影，生成立体效果。
   ```

   

3. **模拟液晶显示屏**

   ```css
   border:none;
   outline:none;  //轮廓
   background-color:#a6af7c;
   border-radius:10px;
   box-shadow: inset 2px 2px 10px #bebebe, inset -2px -2px 10px #fff;
   text-align:right; //字在右边
   font-size:2rem;
   padding:10px;
   ```

   

4. **计算器案例的按键**

   ```css
   width:80px;
   height:80px;
   margin:8px
   ```

   

5. 

