### Sass lecture

1. **安装Sass**

   [官网](https://sass-lang.com/) （Sass.4 即为官方文档翻译后的版本）

   安装 sass：`npm -i -g sass` 

   把 scss 编译成 css 文件：`sass main.scss main.css`。多出的 map 文件是 mapping 两个文件。

   编译可能报错 <font color='red'>.ps1 is not digitally signed. You cannot run this script on the current system.</font> 解决方案：

   ```
   Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
   ```

   

   编译成功后生成了一个新的 .scss 文件，但是每次修改都要重新编译。为了解决这个问题，应使用监听命令：

   ```
   sass --watch style.scss:style.css
   ```

   如果项目中有多个 sass 文件，可以监听整个目录：

   ```
   sass --watch app/sass:public/stylesheets
   ```

   

2. **Sass介绍**

   SASS（syntactically Auesome Style Sheets）有自己语法。SCSS可以沿用CSS语法。SASS只是在css基础上扩展，加入了语法糖。是一个pre-processer，类似于 type script。

   **优势：**

   1. css 重复度太高。颜色/font-family等。sass可以把这些放变量里，重复调用。

   2. css 没有html那样的树状结构，而是平级，因此可读性差

   3. 提高 readability。

      

3. **nested 特性**

   `.container {}` 里面的 flex 可以用语法糖的模式简写，如下，编译后就是普通 css 代码。

   ```scss
   flex: {
       direnction:colunm; 
       wrap:nowrap;
   }
   ```

   

4. **variable 特性**

   Scss 存在的最大意义之一。语法为 `$key: value;` 。key 和 value 可装任何东西，变量中也可用其他变量。

   variable 里面也有 maps（类似于对象）变量。如 `$colors: (main:#521751, secondary:#fa923f)`。取出时用 `map-get($map, $key)`。

   

   

5. **built-in Functions**

   SCSS提供了内置Colors函数，从而更方便地使用颜色。它其实是在原有的 source color 基础上加工。

   CSS原有颜色类型，十六进制、RGB、RGBA、HSL、HSLA和色彩单词。

   ~~~scss
   $color0: green;
   $color1: lighten($color, 15%);
   $color2: darken($color, 15%);
   $color3: saturate($color, 15%);
   $color4: desaturate($color, 15%);
   $color5: (green + red);
   ~~~

   

6. **Partials & better import**

   原生 css 自带的 import：`@import "typography.css";`，打开 Network-All 中发现了2个 css 网络请求，即每个引入的 css 文件都会多请求一次，效率偏低。但是我们依然需要把一个大 css 拆分成多个小 css 文件，以便维护。因此就需要 Sass 的 better import 和 Partial。

   Scss 文件也可以引入另一个 Scss 文件，如 `@import "typography.scss";`，这时编译后的 css 文件中能够发现，原先引入的 `"typography.scss"` 文件也被编译到主文件中了，成为了一个文件。这时 Network 文件中就只有一个 css 文件了。

   

7. **Advanced @media**

   提升 media query。原生 css 中 media query 要定义多个属性，如

   ```scss
   @media (min-width:40rem) {
       html {font-size:125%;}
       .container {padding:3rem 0;}
       .sass-introduction,
       .sass-details {width:30rem;}
   }
   ```

   而在 scss 中，可以把 `@media(){单独项}` 写入对应属性中。

   这样可以把每个选择器中所需要的所有样式全部写在一起。

   

8. **Inheritance**

   Scss 可以实现样式代码复用。需要服用的代码可以放在一个类样式中，然后用 `@entend 类` 复用。如：

   ```scss
   .sass-section {...}
   .sass-introduction {
       @entend .sass-section;
       自身样式
   }
   .sass-details {
       @entend .sass-section;
       自身样式
   }
   ```

   

9. **Mixins**

   定义一些 customized function，实现类似 `map-get()` 和 `darken()` 的功能。定义方式为：

   ```scss
   @mixin name (){}
   ```

   ```scss
   @mixin display-flex (){
       display: -webkit-box;
       display: -ms-flexbox;
       display: -webkit-flex;
       display: flex;
   }
   ```

   调用时使用 `@include mixin-name` 语法：

   ```scss
   @include display-flex();
   ```

   
   
   也可以传参，配合 @content 使用。
   
   ```scss
   @mixin media-min-width($width){
       @media (min-width:$width){
           @content; //可以在@media-min-width时传入属性。
       }
   }
   ```
   
   ```scss
   html {
       font-size:94.75%;
       @include media-min-width(40rem){  //调用
           font-size:125%;
       }
   }
   ```
   
   

