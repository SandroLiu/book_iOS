# 核心动画基础

Core Animation 通过缓存视图的内容到一个容易被绘图硬件操作的位图上来提供更好的性能和动画。除了缓存视图内容外，Core Animation 还定义了一种指定任意可视内容的方法，将内容与视图集成在一起，并将其与所有内容一起进行动画化

Core Animation 使用动画改变view和可视内容，大部分改变是与修改可视内容的属性相关。例如位置、大小、不透明度。

## layer对象提供了绘图和动画的基础
layer是Core Animation的核心。layer 管理关于几何、内容和可视属性，但是不管理显示。一个layer仅仅管理位图周围的状态信息。因此layer可以认为是一个model对象，因为它主要是管理数据的。

### 基于layer的绘图模型
大部分layer不做绘图，相反，layer捕获app提供的内容将其缓存到一个位图。当你改变一个layer的属性的时候，你所改变的是与layer相关联的状态信息。当这个改变触发了一个动画时，Core Animation会将layer的位图和状态信息传递给绘图硬件，绘图硬件使用新的状态信息渲染位图。这样更快。

基于layer的绘图是操作一个静态的位图，与基于view的绘图不同。基于view的绘图，改变自身的时候会引起view的`drawRect:`方法的调用，使用新的参数重绘。这种方法使用CPU在主线程绘制，代价很高。

layer不做绘图，layer保存位图状态信息

### 基于layer的动画

layer对象的数据和状态信息与它内容的显示是分离的。这就让Core Animation可以使用动画改变自身。layer有一些可以使用动画的属性，Core Animation使用帧动画。

### layer的几何学
layer管理自己可视的几何内容，包括内容的bounds，屏幕上的位置，旋转，缩放，或者变换等。layer 有frame 和 bounds

#### lyaer 有两种坐标系
layer使用`基于点`的坐标系和`单位`坐标系。当指定的属性值直接映射到屏幕坐标或必须与其他layer相关时使用`基于点`的坐标系，例如layer的position属性。当属性值和屏幕坐标无关而是与其他值相关时使用`单位`坐标系。例如layer的锚点(anchorPoint)属性

大部分情况使用`基于点`的坐标系是指定layer的尺寸和位置。`bounds`指定了layer自身的坐标系和layer在屏幕上的尺寸。`position`属性指定了layer在父坐标系上的位置。`frame`属性是通过`bounds`和`position`属性推导出来的

`bounds`和`frame`的方向依据底层系统，iOS原点在左上角，OS X 在左下角。如图1-3所示
![](../images/Snip20171206_13.png)

如图1-3，position属性在layer的中间。该属性是一系列基于`锚点`的值而定义的属性中的一个。`锚点`值确定了坐标的起始点。

`锚点` 是一系列使用`单位`坐标系中的一个。Core Animation使用`单位`坐标系展示哪些值随着layer的尺寸改变而改变的属性。`单位`坐标系指定总值的百分比，值的范围是0-1。坐标方向如图1-4，依赖具体的系统
![](../images/Snip20171206_14.png)

#### 锚点影响几何上的操作

可以通过layer的锚点属性访问layer上发生的与锚点相关的几何操作。当操作`position`或`transform`属性时`anchor point`的影响更明显

图1-5展示了锚点`anchor point `如何影响`position`属性的
![](../images/Snip20171206_15.png)
![](../images/Snip20171206_16.png)

图1-6展示了`anchor point`如何影响`transform`的
![](../images/Snip20171206_17.png)
![](../images/Snip20171206_18.png)

#### layer可以在3D上被操作
每个layer有两种`transform`矩阵，可以使用它们操作layer和它的内容。CALayer的`transform`属性定义了想要应用到layer和子layer上的transforms。`sublayerTransform`是操作子layer用的，通常是给一个场景的内容添加一个透明的可视效果时使用。

transfomr通过一个矩阵值乘以坐标值来获得新的坐标值。因为Core Animation可以在三维上操作，每个坐标有4个值，必须乘以一个4x4的矩阵。图1-7表示了Core Animation使用CATransform3D类型的矩阵操作。
![](../images/Snip20171206_20.png)
一般情况下不需要这么复杂的操作，Core Animation提供了一系列的函数操作transforms。同时Core Animation也提供了key-value支持通过一个key paths修改一个transfomr。详细列表查看 `CATransform3D Key Paths`

图1-8 展示了一些通用的矩阵操作配置。使用 identity transform乘以任何坐标都会得到同样的坐标，对于其他transfomation，如何修改坐标完全依赖于你修改的坐标分量的值。例如沿x轴移动，修改tx分量，而ty和tz设为0。对于旋转，需要提供旋转角度的sin和cos的值
![](../images/Snip20171206_21.png)

#### layer trees 反应了动画状态的不同方面

Core Animation 有三种layers 对象的集合，每种集合在layer的内容呈现在屏幕上扮演了不同的角色。
    - model layer tree(layer tree)，在这个tree里，layer对象作为一个model对象，存储动画的目标值。使用这个tree修改属性的值。
    - presentation tree包含动画在运行中的值，动画展现在屏幕上的当前值。不要修改这个对象。可以通过这个tree获取当前动画的值。
    - render tree Core Animation 私有的，真正执行动画。
    
layer tree中每个对象都有一个在presentaiton tree 和render tree中匹配的对象。如图1-10。访问layer tree中对象的` presentationLayer`属性可以获取在  presentation tree 中匹配的对象。这样可以获取当前动画值。
![](../images/Snip20171206_23.png)

> 重要：只有当动画运行时才可以访问presentation tree。layer tree 值是动画完成时的值。

#### Layer 和 View 的关系
Layers 不是 view的一个替代品，Layer 为 view 提供了一些基础的东西。Layer 让绘制view的内容和动画变得容易和更有效。有一些东西是Layer不做的。Layer不处理事件，绘制内容，参与响应者链。

iOS中每个view都有一个Layer，OS X中不是。在有layer的view中推荐操作view而不是layer。在iOS中view是layer一个小的封装，操作layer通常不会有问题，但有时也会有问题。
layer更轻量级，创建layer代价低，可以优化APP