# Category
- category 会覆盖掉类中同名的方法，但不是真的覆盖，只是 category 中的方法会在方法列表的前面
- load方法调用顺序，先调用类的，在调用 category，而 category 的load 方法执行顺序根据编译顺序决定，而 load 调用会找到最后一个编译的 category 的 load 方法
- 因为 category 不能添加实例变量，所以想要为 category 添加属性，可以利用对象关联的方法
