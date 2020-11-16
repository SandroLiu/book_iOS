# swift tips

## `@objc `的用法
在 Swift 代码中，使用`@objc`修饰后的类型，可以直接供 Objective-C 调用。可以使用`@objc`修饰的类型包括：
- 未嵌套的类
- 协议
- 非泛型枚举（仅限于原始值为整形的类型）
- 类和协议中的属性和方法
- 构造器和析构器
- 下标

修饰selector的方法，因为swift是不使用运行时的，selector选择器使用的是运行时方法，通过在方法前添加`@objc`来告诉编译器该方法使用运行时特性

## 什么时候不使用值绑定
- 当修改一个值类型本身的时候，不能使用值绑定，因为值类型的绑定是复制出一个值出来，这个时候修改只会修改复制出来的值，并不能对原值修改
- 例子
```swift
 struct Person {
     var name: String
     var age: Int
 }
 var optionalLisa: Person? = Person(name:"Lisa Simpson",age:8)
 if optionalLisa != nil { // 注意此处不能使用值绑定
    optionalLisa.age += 1
 }
```
 