# 设置Layer 对象

- 使用`layerClass`方法修改view自身的layer的类型

## 提供Layer的内容
layer 是一个管理由app提供的内容的数据对象。使用位图显示内容，有三种方式修改内容
    - 分配一个image给一个layer的`contents`属性(对于内容不变的layer最适合)
    - 赋值一个delegate对象，让delegate绘制layer的内容。(对于内容可能改变和有外界提供内容的layer很适合)
    - 定义一个layer的子类，覆盖绘图方法自己提供内容。

### 提供image给layer
