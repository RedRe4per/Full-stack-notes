### CSS 技巧

1. **网站的文件夹目录设计**

   + index.html

   + src > style.css

   + src > script.js

   + src > assets > video >vidoes  &&  src > assets > images > svgs

     

2. **资源网站**

   视频和图片：https://www.pexels.com/

   svg 图标：https://remixicon.com/   https://fontawesome.com/   https://svgsilh.com/ 图标下载下来用

   

3. **网页设计思路**

   可以采用分层思路：隐藏的 menu 放在最下层，背景图片/视频放在上一层，滤镜放在更上一层，最后是真正的 HTML 主体放在最上层。这里注意的是，分层只需用 z-index 来实现，不需要有 html 层次，也不需把图片/视频放在 css 用 bg 来做。

   掀开隐藏层：z-index 的上层元素（整个上层页面）可以用绝对定位，并且设置之后要拉开的边，如 `right:0;`。这样之后想拉开时再设置 `right:Npx` 就可以了。

   固定高度的网页：不会滚动的单页面网页，高度应该设置为 `min-height: 100vh` 。vh 是所视高度。

   

4. **代码简写与起名**

   创建标签的同时自带类名：`section.showcase`  就会创建  `<section class='showcase'></section>`。

   网站最上面的第一行可以叫 header 或者 nav。里面的每个稍微大点的元素都可以给 class 名。

   多行标签生成：`(li>a>img)*3` 。这种简写后的结构用 tab 键就可以在结构的可输入处跳转。

   随机段落：`Lorem * n` 想要几段就乘多少。

   

5. **视频**

   视频设置：静音 `mute`； 自动播放 `autoplay`； 循环播放 `loop`。

   视频作为背景：

   ```css
   position: absolute;  //一定是absolute，因为背景要占全网页。
   top:0;
   left:0;  //固定absolute的位置
   width:100%;
   height:100%;  //视频分辨率和网页可能不一样，即有上下黑边
   object-fit:cover;  //分辨率不同的解决方案。可以去黑边，并且根据网页宽高的变化而改变背景视频。
   opacity:0.8;  //让视频透明，上层文字就能显示了。
   z-index:0;  //视频在最底层。此设置没必要写。
   ```

   滤镜：可以直接给视频一个 html 同级的 div，class='overlay'。之后覆盖在视频上层。

   ```css
   position: absolute;  
   top:0;
   left:0;  
   width:100%;
   height:100%;  //前面设置与视频一致
   background-color:var(--overlay-color)  //主题色，最好以变量形式设置。但是默认是不透明的。
   mix-blend-mode:overlay;  //会把主题色，视频，和文字层的背景色叠加。
   ```

   ```css
   background-color: rgba(255,255,255,0.5)  //另一种处理滤镜色方式。不适合处理主题色，颜色会虚掉。
   ```

   

6. **按钮**

   一般按钮不用 button 来做，而是用 a 标签来做。a 标签也是透明的（即 inline 里可以放 block），因此可以 a 标签里面套 div。<font color='lightgrey'>没有具体 link 的按钮就 href='#'，点击刷新当前页面。</font>

   <font color='red'>用 a 标签做按钮需要保证文字不能缩太小，也不能换行。因此要设置为 `display:inline-block;`。</font> 这里面 inline 部分的特性是，多个 a 在窗口缩小时会流动到下一行；而 block 部分特性是 a 内部的文字不会因为挤压而变小或换行。即外表看起来像 inline，但是内在是 block。注意如果是 a 标签里面套 img 图标，也需要设置成 inline-block 元素。

   a 标签做按钮也需要去掉下划线：`text-decoration: none;`。

   文字中每个字母间隔：`letter-spacing: 2px;`。

   按钮要显得大一些：`padding: 10px 30px;`。

   鼠标移入有变化：`cursor: pointer`。

   

7. **text群**

   一般网站会有字体样式不同的 text 群堆叠在一起。实际做起来可以用一个 div.text 包裹住这些 text 群，然后再用 h2，h3，p 等标签细分。这样的好处是 div.text 可以作为一个整体的元素，和网站的 header/nav 和 footer 一起布局。

   大小写问题：应该在 css 中用 `text-transform: uppercase;` 改，而不是直接大写写在 html 中，因为日后可能会修复。

   p 段落中的文字可能会需要限宽，即可以缩小但不能铺的太长。`max-width:Npx;`

   

8. **svg与可切换图标**

   <font color='green'>svg 图片</font> 用的时候先下载，然后直接在 html 用 img 标签即可。

   <font color='green'>可切换的图标</font> 比如 menu 和 close，通常不在 html 里面加。即固定图标写入 html，可变图标写入 css，写的时候用 `background: url()` 即可。切换功能可用 `.active`，把另一个图标的链接和配置项写入即可。

   这时由于图标成了背景，会 repeat 并且不居中。因此要用：

   ```css
   background-repeat: no-repeat;  //不重复
   background-size: 30px;  //svg 矢量图大小随意改，并且下载的矢量图大小变化很大。
   background-position: center;  //居中
   ```

   <font color='red'>svg 图标有一种特殊的黑白变色</font>，用 `filter:invert(1);` 黑白取反颜色。

   

9. **暂时隐藏某个元素**

   css 中 `display: none`。或者直接 html 代码注释掉。

   

10. **更改css字体**

    在 google fonts 网站中，右上角搜索 Poppins。可以把所有字体全选，就全加载在 Poppins 中了。之后，直接引入 Poppins 的 link：`@import ...` 。这只是引入进了 css，但是还没用。

    更改字体前应该先 `* {box-sizing: border-box;}`。这是因为假如 width:100px，border:3px，整体长度就是 106px 了。设置了 box-sizing 后，整体长度依然是100px，即 border 不会超过宽度。

    ```css
    * {box-sizing: border-box; 
        margin:0;
        padding:0;
        font-family:'Poppins', sans-serif; //从左向右找字体。前面可能没有网络所以导致用不了。
    }
    ```

    这里不写在 body 中的原因是，body 里面的元素是继承，而 * 是直接选择所有元素。假如 body 下的某一层 margin 改掉了，那么它的在下层就继承了新的 margin，导致不确定性。

    

    在某个子元素中更改字体：`font-size` 属性一般用 rem 单位，如 5rem；但是 `line-height` 不要用 rem，应该用 em，如 1em。因为 rem 是根据浏览器默认字体大小走，而在某个子元素中改了 `font-size` 后（例如 responsive），它下面的 em 就会根据 `font-size` 的大小走。如果设置成了 rem，会导致限高错误。

    ```css
    font-size:5rem;
    font-weight:800;
    line-height:1em;
    ```

    

    有一种做法是设置 `:root{font-size:62.5%;}` 。这样就把默认的 16px 变成了 10px，1rem=10px，方便计算，例如 80px 的宽度直接写 8rem 就行。同时，需要改大小的时候直接改 font-size 就可以。这种方法是大型项目中的标配。

    

11. **flex中的元素脱离文档流**

    flex中的元素如果用了 absolute，也是可以脱离文档流的。此时，只有剩下的 flex 元素遵守布局。

    

12. **变量**

    变量用 `--` 来定义，用`var(--varName)`来引用，并且可以被 JS 拿到。

    ```css
    :root {  //在css最上的root里声明--变量并赋值
        --logo-size:60px;
    }
    ```

    ```css
    width:var(--logo-size) / 2;  //引用变量 
    ```

    

13. **.active在css中的处理**

    html 中用 `.active` 来操作元素，比如给元素添加一个 `.active` 类（元素可以有多个类）。同时，可能有多个 `.active` 来操作多个元素。为了不起多个名字，可以在 css 中使用 `.toggle.active {}` （两个选择器中无空格，并列关系）来选取特定的 `.active`。

    

14. **可互动元素的动态效果**

    a 按钮元素，鼠标移入时按钮拉长：

    ```css
    a {transition:0.2s;}  //拉长有个动画过程
    ```

    ```css
    a:hover {letter-spacing: 6px;}  //鼠标移入时拉长
    ```

    

    a 元素按钮，鼠标移入时按钮跳动：

    ```css
    .social li a {transition:0.5s;}
    ```

    ```css
    .social li a:hover{
        transform:translateY(-10px);  //Y轴默认方向向下，而向上跳动需要负值。
    }
    ```

    

    上层页面收缩以显示隐藏的下层页面：

    ```css
    .showcase {transition:0.5s ease-in-out;}  //ease-in-out是柔和缩放。
    ```

    

15. **去掉 li 的默认样式**

    在 ul 或者 ol 中，设置 `list-style: none;`。

    

16. **揭开隐藏的最下层页面**

    隐藏的页面一般只占 viewport 的一部分，因此需要宽度。注意这个宽度之后要用到多次，因此最好设为变量 `--menu: 300px` 。

    ```css
    .showcase.active {  //原本的上层页面从右侧被掀开左移。
        right:var(--menu-width);  
        width: calc(100%-var(--menu-width));  //非统一单位时的计算。如果不改，会导致页面超出左边界。
    }
    ```

    隐藏界面的文字依然要用绝对定位，并且为了可以让文字的 div 宽度和隐藏界面匹配，应该用 

    ```css
    .menu {width: var(--menu-width);}
    ```

    

17. **切换按钮的 JS**

    引入 JS 文件：body 最下方，`<script src=''/>`。

    按钮和需要变化的元素（如上层页面）都需要进行 DOM 操作。

    切换 active 类：`menuToggle.classList.toggle('active')` 。

    

18. **伪元素**

    在某个元素前/后使用，需要有 content 和 color 属性。

    ```css
    .home>.text>h3::after {
        content: "abc";
        color: #c66;
    }
    ```

    装饰性伪元素：

    ```css
    .ribbon::after {
     content: "Look at this orange box.";
     background-color: #FFBA10;
     border-color: black;
     border-style: dotted;
    }
    ```

    

19. **div里面不能有文字**
