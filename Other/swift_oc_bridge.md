# Swift与OC混合开发

此文档中`Swift`与`OC`混合开发指的是在`Swift`文件中使用`OC`类，和在`OC`文件中使用`Swift`类，与是`Swift`工程还是`OC`工程无关。

## Swift文件中使用OC

- 桥接文件名为`工程名-Bridging-Header.h`，此桥接文件是用来在Swift文件中使用OC类的。

#### 创建桥接文件
- 自动创建桥接文件，在OC工程中创建`Swift`文件会自动弹出创建桥接文件选项
![](/assets/Snip20201104_2.png)
![](/assets/Snip20201104_3.png)

#### 使用
- 在桥接文件中引用想要在`Swift`中使用的`OC`类
![](/assets/Snip20201104_4.png)
- 在`Swift`中使用OC类
![](/assets/Snip20201104_5.png)

## OC文件中使用Swift

- 在`OC`文件中引入`import "工程名-Swift.h"`，引入后直接使用`Swift`类后即可
![](/assets/Snip20201104_8.png)

- 注意工程名以`Swift`开头，引入`工程名-Swift.h`可能导致编译失败，