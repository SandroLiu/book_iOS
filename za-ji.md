## OC 中 NULL、nil、Nil、NSNull 的定义及不同

- NULL：本质上是`(void *)0`
    - 使用：`NULL`一般用于表示 C 指针空值，例如：
    
```obj
int *pointerToInt = NULL;
char *pointerToChar = NULL;
struct TreeNode *rootNode = NULL;
```
- nil：yu`NULL`一样也是`(void *)0`
    - 使用：用于表示指向 OC 对象的指针为空，例如：
    
```obj
NSString *someString = nil;
NSURL *someURL = nil;
id someObject = nil;
if (anotherObject == nil) // do something
```
- Nil：本质上是`(void *)0`
    - 使用：用于表示指向 OC 类(Class) 类型的指针为空，例如：

```obj
Class someClass = Nil;
Class anotherClass = [NSString class];
```
- NSNull：是一个 OC 对象，是一个用于表示空值的类，一般用于在集合对象中保存一个空的占位对象。
