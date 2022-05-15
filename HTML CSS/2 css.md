# CSS

1. 居中，可以直接设置完 width 之后 margin: auto。这样就可以直接在父元素居中

2. 图片，给了 width 之后，height可以直接auto，默认图片比例。

4. 元素用 margin 好一点，比起 padding

5. 固定位置 position：fix。跟屏幕视野（viewport）定位。

   固定定位的上导航栏可以写成 width：300%，min-with：/max-width，left：50%，transform：translateX(-50%)。左移宽度一半，并且把元素定位到屏幕中间。如果不写 left 和 transform 也能实现，但是写了是最优解。

6. position：absolute

   1. 用法，上级要有 position：relative

   2. absolute的元素不在元素流中。

   3. 没给 relative 就相对于 body了。

   4. 例子，搜索框点击后下拉弹窗，就是典型的 absolute。

   5. 有隐患：要测不同屏幕，如果有break point多的话（5个以上？）就没办法了。而且都是脱离文档流的，适配不同屏幕会有问题。

      因此，尽量不要用 position absolute，而是优先考虑 flex；不能做的话再用 position。

7. position：sticky

   position: -webkit-sticky

   用于浏览器适配的。元素根据鼠标滚轴，如果滚的超出屏幕范围，元素依然在视野中。top等可以设置距离屏幕边界的最大位置。

8. %单位是 relative to the parent element

9. normalize.css 下载到 head 里面，目的是让所有浏览器的元素默认样式一致。

   目前应该已经被淘汰了，用 react 就行。

11. -webkit- 前缀是为了兼容老版本浏览器。



----kitman的tut03----

1. background image 的缺点：图片对SEO不利，做定位有时会有问题。但是就可以不用绝对定位，不用脱离文档流，好做responsive。如果左边文字右边图片（tutorial例子），viewport缩小后就可以图片变到文字上/下面。（用 flex 调整）。
2. 不要为了加 css 而特意加 div，这样符合 seo 标准
3. button尽量少用，用 a 标签就行。 a 是 inline，但是内部可以放 div。
4. card作业，图片用 background 比较好。如果需要把背景图片变暗，方案1是图片用img写在html里（不好），方案2是用 Photoshop 自己修图（好），方案3是用两个background image，黑色透明放上面。通常是ui已经做好了。
5. Figma里面，不能抄 position absolute，align。这些是 figma里面的配置，会影响 responsive。
6. 排版优先用 flex，用不了再用 absolute。会有脱离文档流，不能 responsive的问题。
7. 元素位置超过background img 尺寸？可以设置 background-size：300px 100px。还不行的话，如果不想让background变型，还可以设置background position的px，能把图片往上挪。



------

1. 只读不能填的input，加 readonly属性。