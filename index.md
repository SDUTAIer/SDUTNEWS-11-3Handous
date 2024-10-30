## SDUTNews-立体网页设计及CSS动画进阶
![](./img/CSS.gif)
### 上回说到
当我们使用`:hover`时，可以设置鼠标悬停样式以及动画持续时间

`:hover`中还有一个参数是`动画时间函数`：CSS 属性受到`transition effect`的影响，会产生不断变化的中间值，而`CSS transition-timing-function`属性用来描述这个中间值是怎样计算的。实质上，通过这个函数会建立一条`加速度曲线`，因此在整个`transition`变化过程中，变化速度可以不断改变

`transition-timing-function`有如下可选参数,这些参数我们叫做`贝塞尔曲线(bezier)`

### 平滑过度
bezier曲线(函数)在后续的animation动画中也有应用

1. `ease`
>![](./img/ease.png)

>这个参数会使过度动画呈现`慢-快-非常慢`的效果

2. `linear`
>![](./img/linear.png)

>这个参数会使过度动画`匀速变化`(默认值)

3. `ease-in`
>![](./img/ease-in.png)

>这个参数会使过度动画从开始发生过度到过度结束的过程`先慢后快`的效果

4. `ease-out`
>![](./img/ease-out.png)

>这个参数会使过度动画呈现从过度完成到回到原状`先慢后快`的效果

5. `ease-in-out`
>![](./img/ease-in-out.png)

>这个参数会使过度动画无论是开始过度还是过度开始恢复原状时均`先慢后快`

### 步进帧过度
步进帧过度看起来的效果是一帧一帧动的，相较于平滑过度帧率更低，多用于配合`animation`实现打印动画，应用范围较窄

```CSS
transition-timing-function: step(Frame rate, start/end);

Frame rate:帧率，动画要在多少帧完成

start:动画从一开始就开始发生变化

end:动画在最后发生变化(类似加了transition-delay)
```


## 立体网页基础

### 伪元素`::before`和`::after`

1. `::before`
>"::before" 伪元素可以在元素的内容前面插入新内容

2. `::after`
>":after" 伪元素可以在元素的内容之后插入新内容

伪元素和普通的标签一样，可以设置CSS样式，同样定位也是可以生效在伪元素上的，比如
![](./img/weilei.png)
我们给`::before`设置absolute定位，`::before`会找到上一级相对定位的div，跟我们在父div里面设置子div绝对定位是一样的效果

同样的`::after`也是一样的效果

所以我们可以使用`::before`和`::after`+`定位`的组合可以实现3D立体效果,具体怎么实现呢？

这里我们还需要引入一个新东西，transform里面的3D旋转函数`skew()`即`transform: skew(xxdeg); `

1. `skewX()`设置X方向上的偏移量:x轴水平向右为正向

>`transform: skewX(45deg);`

>![](./img/45deg.png)

>`transform: skewX(-45deg);`

>![](./img/fu45deg.png)

2. `skewY()`设置Y方向上的偏移量：y轴垂直向下为正向
>`transform: skewY(45deg);`

>![](./img/y45deg.png)

>`transform: skewY(-45deg);`

>![](./img/y-45deg.png)


### 实现3D立体盒子动画(视频展示)
大致步骤：
1. 一个大div,设置X或Y轴偏移量，里面嵌套n个小div（n的个数看你要堆放几个立体盒子，如果只有一个立体图形，就嵌套一个div即可）
2. 对小div设置伪元素`::before`和`::after`
3. 小div相对定位，伪元素绝对定位
4. 修改伪元素的`top`和`left`属性,并添加X或Y轴方向上的偏移量，实现3D盒子封闭效果，需要结合`transition-origin`
5. 多个立体盒子的需要对小div设置`z-index`属性，突出上下层关系
6. 对小div设置`:hover`伪类，

>yes