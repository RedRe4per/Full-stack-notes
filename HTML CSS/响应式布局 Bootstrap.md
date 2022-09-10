### 响应式布局 Bootstrap

1. **响应式布局**

   一个页面对应多种设备，设备屏幕/pc网页大小改变时，自动改变页面布局（而不是元素/文字大小）。

   因此不需要单独写移动端页面。

   

2. **响应式开发**

   1. 响应式开发原理

      就是使用媒体查询针对不同宽度的设备进行布局和样式的设置，从而适配不同设备的目的。

      |         设备划分         | 尺寸区间（尺寸指宽度） | 布局容器（通常）宽度设置 |
      | :----------------------: | :--------------------: | :----------------------: |
      |     超小屏幕（手机）     |         <768px         |           100%           |
      |     小屏设备（平板）     |    >=768px ~ <992px    |          750px           |
      |  中等设备（桌面显示器）  |   >=992px ~ <1200px    |          970px           |
      | 宽屏设备（大桌面显示器） |        >=1200px        |          1170px          |

      

   2. 响应式布局容器

      响应式需要一个父级作为布局容器，来配合子级元素来实现变化效果。

      原理就是在不同屏幕下，通过媒体查询来改变这个布局容器的大小，再改变里面子元素的排列方式和大小，从而实现不同屏幕下，看到不同的页面布局和样式变化。

      布局容器常见宽度如上表。容器比屏幕少一点是让页面居中对齐两侧空白，好看一点。

      可以自己用媒体查询写 `.container {}`，分四种情况写。

      

3. **快速开发与Bootstrap**

   概念类似于毛坯房，不自己装修，找装修公司用现成模板来做。即用响应式布局工具：Bootstrap前端框架。

   **Bootstrap**：来自于 Twitter（因此有浓重的 twitter 风格），是目前最受欢迎的前端框架，Bootstrap 是基于 HTML，CSS 和 JS 的，它简单灵活，使 Web 开发更加快捷。[官网](www.bootcss.com) [中文官网](getbootstrap.com) [推荐使用](bootstrap.css88.com)

   公司项目中一般不会用 Bootstrap，而是自己的组件库。

   

4. **Bootstrap使用**

   1. <font color='blue'>创建文件夹结构</font>

      官网下载之后，复制 css/fonts/js 三个文件夹，之后在 index.html 同级创建 bootstrap 文件夹，放入三个复制文件夹。

   2. <font color='blue'>创建 html 骨架结构</font>

      bootstrap 官网，找到基础文档并复制进 html 文档。

   3. <font color='blue'>引入相关样式文件</font>

      ```html
      <Link rel="stylesheet" href="bootstrap/css/bootstrap.min.css">
      ```

      引入后不需要再写 Normalize.css，Bootstrap 内部已经做了引入。

      也可以直接 cdn 引入，记得引入 css 和 js 部分。在 Bootstrap 官网中 get start 中有。

   4. <font color='blue'>写内容</font>

      Bootstrap 是通过<font color='red'>类名</font>来控制样式的。在官网找到样式，复制即可。

      想在 Bootstrap 样式的基础上修改，可以添加类名修改。如果自己写的样式无效，可能是权重不够。

      

5. **Bootstrap布局容器**

   Bootstrap 需要为页面内容和栅格系统包裹一个 `.container` 容器：`<div class="container">` ，Bootstrap 预先定义好了这个类，叫 `.container` ，它有两个类。

   1. <font color='blue'>container 类</font>

      响应式布局的容器，<font color='red'>固定宽度</font>：大屏宽度定位1170px，中屏宽度定为970px，小屏宽度定为750px，超小屏为100%。

   2. <font color='blue'>container-fluid 类</font>

      流式布局容器，<font color='red'>100%宽度</font>；占据全部视口 viewport 的容器；<font color='red'>适合于单独做移动端开发</font>。

      

6. **Bootstrap 栅格系统**

   栅格系统（grid systems）指将页面布局划分为等宽的列，然后通过列数的定义来模块化页面布局。

   栅格系统和 rem 有些相似，rem 是把屏幕整体划分为若干份，栅格系统是把页面内容划分成若行列。Bootstrap 就是通过行（row）和列（column）的组合来创建页面布局，程序员写的内容就放入了这些创建好的布局中。

   Bootstrap 提供的栅格系统是响应式+移动设备优先的，随着屏幕或 viewport 尺寸的增加，系统会自动分为最多12列。这把 container 分成了12等份，当屏幕变小后，页面 viewport 还是12份，只是元素会变小。

   

   例如，要做一个导航栏，其背景颜色是和屏幕宽度相同（100%），内容只占屏幕宽度的一部分且居中。这时就可以在最外层包一个 div 并且宽度100%，之后里面放一个 container，用12等份来装导航内容。也就是说，需要一行分成若干份的情景都需要用 container，不分份就不用。

   

