使用CSS3开启GPU硬件加速提升网站动画渲染性能
======================================

现在的网页多多少少都会有一些动画或者微动效，那么如何来提高页面的动画渲染性能将是我们所面对的比较重要的话题。今天就来记录下如何用css3开启浏览器的GPU硬件加速，来提升网站动画渲染性能。

CSS3为开发者们开发动画效果大大提升了效率，但有些动画设计得DOM元素比较多，会出现“卡卡”的感觉，为动画DOM元素添加CSS3样式`-webkit-transform:transition3d(0,0,0)`或`-webkit-transform:translateZ(0)`，这两个属性都会开启GPU硬件加速模式，从而让浏览器在渲染动画时从CPU专项GPU，其实说白了这是一个小技巧，也算是一个hack，`-webkit-transform:transition3d`和`-webkit-transform:translateZ` 其实是为了渲染3D样式，但我们设置值为0后，并没有真正使用3D效果，但浏览器却因此开启了GPU硬件加速模式。

这种GPU加速再当今PC机及移动设备上都已普及，在移动端的性能提升是相当显著的，所以建议大家在做动画时，可以尝试一下开启GPU硬件加速。

当然也可以这样开始所有浏览器的GPU硬件加速：

```css

webkit-transform: translateZ(0);
-moz-transform: translateZ(0);
-ms-transform: translateZ(0);
-o-transform: translateZ(0);
transform: translateZ(0);

```

或者

```css

webkit-transform: translate3d(0,0,0);
-moz-transform: translate3d(0,0,0);
-ms-transform: translate3d(0,0,0);
-o-transform: translate3d(0,0,0);
transform: translate3d(0,0,0);

```

通过 **-webkit-transform:transition3d/translateZ** 开启GPU硬件加速之后，有些时候可能会导致浏览器频繁闪烁或抖动，可以尝试以下办法解决：

```css

-webkit-backface-visibility:hidden;
-webkit-perspective:1000;

```

### 通过-webkit-transform:transition3d/translateZ开启GPU硬件加速的适用范围：

*	使用很多大尺寸图片（尤其是png24图）进行动画的页面
*	页面有很多大尺寸图片并且进行了css缩放处理，页面可以滚动。
*	使用**background-size:cover**设置大尺寸背景图，并且页面可以滚动时[Improve scroll performance of Chrome when using background-size: cover](https://coderwall.com/p/j5udlw/improve-scroll-performance-of-chrome-when-using-background-size-cover)。
*	编写大量DOM元素进行CSS3动画（transition/transform/keyframes/absTop&Left）
*	使用很多PNG图片拼接成CSS Sprite时

## 总结：

通过开始GPU硬件加速虽然可以提升动画渲染性能或解决一些棘手问题，但使用仍需谨慎，使用前一定要进行严谨的测试，否则它反而会大量占用浏览网页用户的系统资源，尤其是移动端，肆无忌惮的开启GPU硬件加速会导致大量消耗设备电量，降低电池寿命等问题。

## 参考链接：

*	http://blog.csdn.net/hsany330/article/details/50925260
*	http://www.feelcss.com/css3-gpu.html
