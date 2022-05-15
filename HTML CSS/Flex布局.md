### Flex 布局

1. **flex布局特点**

   传统布局：兼容性好，布局繁琐，局限性，不能在移动端很好布局。flex 是一种一维布局。

   flex弹性布局：操作方便，布局简单，移动端好用，PC端浏览器支持情况较差，IE11以下不支持/部分支持。

   建议：PC端页面布局用传统布局，移动端/不考虑兼容性问题的PC端，用 flex 布局。

   

2. **flex布局原理**

   flex 是 flexible box 的缩写，弹性布局，用来为盒状模型提供最大灵活性，任何一个容器都可指定 flex 布局。采用 flex 布局的元素，称为 flex container；它的所有子元素自动成为容器成员，称为 flex item。

   父元素设定 flex 布局之后，子元素的 float、clear 和 vertical-align 属性将失效。（浮动已被淘汰。并且flex可以让元素垂直居中，因此 vertical-align 失效）。

   总结：就是通过给父盒子添加 flex 属性 `display:flex;`，来控制子盒子的位置和排列方式。注意和 `display:block` 区分。

   

3. **flex布局父项常见属性**

   + <font color='blue'>flex-direction</font>：设置主轴的方向<font color='lightgrey'>（不重要）</font>

     <font color='green'>主轴和侧轴</font>：行和列，x 轴和 y 轴。默认主轴水平向右，侧轴垂直向下。主轴和侧轴是会变化的，就看 flex-direction 设置谁为主轴，剩下的就是侧轴。<font color='red'>而我们的子元素是根据主轴来排列的</font>。例如： `display:flex; flex-direction: row;`

     老师推荐

     

     |     属性值     |       说明       |
     | :------------: | :--------------: |
     |      row       | 默认值，从左到右 |
     |  row-reverse   |     从右到左     |
     |     column     |     从上到下     |
     | column-reverse |     从下到上     |

     

   + <font color='blue'>justify-content</font>：设置主轴上的子元素排列方式

     justify-content 属性定义了 flex item 在<font color='red'>主轴</font>上的对齐方式，使用前要先确定主轴。

     |    属性值     |                            说明                             |
     | :-----------: | :---------------------------------------------------------: |
     |  flex-start   |        默认值，从头部开始，如果主轴是x轴，则从左到右        |
     |   flex-end    |                       从尾部开始排列                        |
     |    center     |         在主轴居中对齐（如果主轴是 x 轴则水平居中）         |
     | space-around  |                   平分剩余空间（不贴边）                    |
     | space-between | 先两边贴边，再平分剩余空间（<font color='red'>重要</font>） |

     

   + <font color='blue'>flex-wrap</font>：设置子元素是否换行

     默认情况下，项目都排在一条线（轴线）上。flex-wrap 属性定义，flex 布局中默认是不换行的。如果子元素宽度累计超过容器，会自动缩小子元素宽度，放在父元素里。

     如果不想要自动缩小子元素，希望多余的子元素自动换行，可以用 `flex-wrap: wrap` 属性。

     |    属性值    |              说明              |
     | :----------: | :----------------------------: |
     |    nowrap    |         默认值，不换行         |
     |     wrap     |              换行              |
     | wrap-reverse | 换行，并且子元素从对角线对调。 |

     

   + <font color='blue'>align-items</font>：设置<font color='red'>侧轴</font>上的子元素的排列方式（单行）

     如果只是想让元素在单一轴上布局，之前的 flex-direction 就够用。但是如果想让元素在主轴+侧轴上同时布局（如主轴居中+侧轴居中），就需要 align-items 了。

     |   属性值   |                             说明                             |
     | :--------: | :----------------------------------------------------------: |
     | flex-start |                           从上到下                           |
     |  flex-end  |                           从下到上                           |
     |   center   |                   挤在一起居中（垂直居中）                   |
     |  stretch   | 默认值？拉伸至父元素高度（<font color='red'>用的时候子元素不要给高度</font>） |
     |  baseline  |                       对齐内容物的基线                       |

     

   + <font color='blue'>align-content</font>：设置<font color='red'>侧轴</font>上的子元素的排列方式（多行）

     用于布局 align-items 中不能实现的需求。align-items 只能上沿/下沿/居中对齐，没有 justify-content 里的 space-around 等。

     align-content 设置子项在侧轴上的排列方式，并且<font color='red'>只能用于子项出现换行的情况（多行）</font>，单行下是无效果的。

     |    属性值     |                  说明                  |
     | :-----------: | :------------------------------------: |
     |  flex-start   |          在侧轴的头部开始排列          |
     |   flex-end    |          在侧轴的尾部开始排列          |
     |    center     |             在侧轴中间显示             |
     | space-around  |         子项在侧轴平分剩余空间         |
     | space-between | 子项在侧轴先分布在两头，再平分剩余空间 |
     |    stretch    | 默认值，设置子项元素高度平分父元素高度 |

     

     **align-content 和 align-items 区别**

     1. align-items 适用于单行情况下，只有上对齐，下对齐，居中和拉伸。
     2. align-content 适应于换行（多行）的情况下，单行无效，可以设置上对齐，下对齐，居中，拉伸以及平均分配剩余空间等属性值。

   

   + <font color='blue'>flex-flow</font>：复合属性，相当于同时设置了 flex-direction 和 flex-wrap

     把设置主轴方向 flex-direction 和是否换行 flex-wrap 简写。

     ```css
     flex-flow:row wrap;
     ```

     

   + <font color='blue'>gap</font>：子元素之间的 margin。

     与 margin 的区别是直接可以让所有 items 继承 gap，而不是每个 items 都写 margin。

     

4. **flex布局子项常见属性**

   1. <font color='blue'>flex 子项目占的份数</font>

      flex 属性定义子项目分配<font color='red'>剩余空间</font>，用 flex 来表示占多少<font color='red'>份数</font>。例如做带搜索的导航栏，左右小按钮固定，中间搜索栏自适应。例如：

      ```css
      section {	/*父元素*/
          display:flex
      }
      section div:nth-child(1) {   /*固定大小，不用写flex*/
          width:100px;
          height: 150px;
      }
      section div:nth-child(3) {   /*固定大小，不用写flex*/
          width:100px;
          height: 150px;
      }
      section div:nth-child(2) {    /*1分就是所有空余空间，自适应*/
          flex:1
      }
      ```

      

      父元素中的三个子元素平分宽度，如

      ```css
      p {
          display:flex;
          width:60%;
          height:150px;
      }
      p span {flex:1}   /*不用给宽高，直接分3等分，每个各占一份。没给宽度，它们的宽度和就是父元素宽度*/
      ```

      不平均分配元素宽度，如

      ```css
      p {
          display:flex;
          width:60%;
          height:150px;
      }
      p span:nth-child(2) {flex:2}   /*2号子元素占两份，这里是50%，其他两个盒子1份，各25%*/
      ```

      

   2. <font color='blue'>align-self 控制子项自己在侧轴的排列方式</font>

      align-self 属性允许单个项目有与其他项目不一样的对齐方式，可覆盖 align-items 属性。

      默认值为 auto，标识继承父元素的 align-items 属性，如果没有父元素，则等同于 stretch。

      ```css
      section div:nth-child(1) {   
          align-self:flex-end;   /*单独一个子元素与其他子元素布局不同*/
      }
      ```

      

   3. <font color='blue'>order 属性定义子项的排列顺序（前后顺序）</font>

      数值越小，排列越靠前，默认为0。注意，和 z-index 不一样。

      ```css
      section div:nth-child(2) {   
          order:-1;   /*靠数字大小来排序*/
      }
      ```

      

   4. <font color='blue'>flex-basis、flex-grow、flex-shrink</font>

      意为子元素在父元素宽度<font color='red'>足够</font>的情况下，伸展的比例；或者父元素宽度<font color='red'>不足</font>的情况下，压缩的比例。

      flex-grow：子元素伸展比例分配，预设值为0，不可负数。如果值为1，就是固定死的不能再放大了。

      flex-shrink：子元素压缩比例分配，预设值为1，不可负数。如果值为0，就是固定死的不能再缩小了。

      flex-basis：子元素基本大小，预设值为 auto。它不是一个固定死的执行的值，而是一个推荐值，即基准值；真正的值是由 grow 和 shrink 决定的。如果 `flex-basis: 0px` ，就固定死大小不能缩放了。

      ```css
      .red{ 
        flex-grow: 1;
        flex-shrink: 1;
        flex-basis: 100px;
      }
      .blue{
        flex-grow: 2;
        flex-shrink: 2;
        flex-basis: 100px;
      }
      ```

      

5. **练习**

   https://flexboxfroggy.com/#zh-cn

   http://www.flexboxdefense.com/

   http://tom.infinityfreeapp.com/html/shapes.html

   

6. **详细教程**

   https://css-tricks.com/snippets/css/a-guide-to-flexbox/
   
   