# 响应与事件

当用户手指触摸屏幕后，iOS系统需要确定第一响应者，确定顺序是由上至下的

`Application`->`Window`->`Controller`->`根视图`->`父视图`->`子视图`，
事件的响应顺序是由下至上，正好相反。

## 确定响应者

开发者一般关心的是`View`如何确定响应，要判断一个`View`能否响应事件，`UIKit`提供了`命中测试`方发。

> \- (UIView *)hitTest:(CGPoint)point withEvent:(UIEvent *)event;

`View`在该方法内先判断自己能否响应该事件，如果自己不能响应则返回`nil`。如果自己能响应则查看有没有子视图响应该事件，如果有子视图则返回子视图，没有子视图则返回自己，`hitTest`方法内部实现如下：

1. 判断当前控件能否接收事件，满足一下任意一点则不能接收事件，返回`nil`
    - userInteractionEnabled 为 NO
    - 控件隐藏
    - alpha &lt = 0.01
2. 判断点在不在自己身上，如果不在自己身上则返回`nil`。

```objc

    if ([self pointInside:point withEvent:event] == NO) {
        return nil;
    }
    
```

3. 查看子视图能否响应，先将坐标点转换到子视图坐标系内，在调用子视图 `hitTest`方法，查看是通过遍历子视图，并且是从后往前遍历，既后添加的子视图先遍历

```objc
    // 从后往前遍历自己的子控件
    NSInteger count = self.subviews.count;
    for (NSInteger i = count - 1; i >= 0; i--) {
        
        UIView *childView = self.subviews[i];
        
        // 把当前控件上的坐标系转换成子控件上的坐标系
        CGPoint childP = [self convertPoint:point toView:childView];
        UIView *fitView = [childView hitTest:childP withEvent:event];
        if (fitView) {
            return fitView;
        }
    }
```

## 应用

正常情况下，如果子视图超出父视图，点击超出部分是不能响应事件的，我们可以通过重写`hiteTest`方法实现点击超出部分也能点击。

```objc
- (UIView *)hitTest:(CGPoint)point withEvent:(UIEvent *)event
{
    // 想要实现点击button上的点时交给button处理
    
    // 1. 将point转换到button的坐标系
    CGPoint btnP = [self convertPoint:point toView:self.btn];
    
    // 2. 判断btn在不在button上
    if ([self.btn pointInside:btnP withEvent:event]) {
        // 点在button上则交给button处理
        return self.btn;
    }
    else
    {
        return [super hitTest:point withEvent:event];
    }
}
```