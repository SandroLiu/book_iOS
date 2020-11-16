#相等性判断

## ==
使用`==`判断对象是判断两个对象的指针是否相等，即两个对象是否指向同一个地址

## isEqual
`isEqual` 是NSObject提供的一个协议来判断两个对象是否相等，子类可以根据自身情形实现自定义的相等判断。默认判断是`==`即地址判断。
一般实现`isEqual`时有几个要素需要考虑：
- isEqual 相等则 两个对象的hash值相等
- 两个对象的hash值相等，isEqual不一定相等

OC中有许多类似NSString、NSDictionary、NSArray等已经提供了更高层次的判断方法，那些方法执行更快。

OC中NSString已经修改了isEqual的默认实现，据我推测应该是调用了`-isEqualString`方法

## containObject
`containObject`是用来判断一个对象在不在数组中的方法，这个方法会调用每个对象的`isEqual`方法，如果有相等的就认为在数组中，否则就没有