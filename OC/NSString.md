# NSString

## 字符串本地化

#### NSLocalizedString

　　`NSLocalizedString`这个宏是字符串本地化的核心工具。它还有三个鲜为人知的变体：  
`NSLocalizedStringFromTable`  
`NSLocalizedStringFromTableInBundle`和  
`NSLocalizedStringWithDefaultValue`。这些宏最终都调用`NSBundle`的`localizedStringForKey:value:table:`  
方法来完成任务。 
　　使用 NSLocalizedString 宏的时候，第一个参数就是为每个特殊字符串指定的键值（key）。   
　　本文推荐使用如下的命名空间方法：

```obj
NSLocalizedString(@"activity-profile.title.the-run", nil)
NSLocalizedString(@"home.button.start-run", nil)
```
　　这样的键值可以区分应用中不同地方出现的单词，同时提供具体的上下文，比如是标题中的或者按钮中的。上面的例子里我们为了简便忽略了第二个参数，实际使用中如果键值本身没有提供清晰的上下文说明，你可以将进一步的说明作为第二个参数传入。同时请确保键值中只含有 ASCII 字符。

## 字符串解析
#### 正则表达式
匹配如下表达式
> backgroundColor = #ff0000

- `\\w+`，它的意思是匹配任何一个数字、字母或者是下划线至少一次（\\w 代表匹配任意一个数字、字母或者是下划线，+ 代表至少匹配一次）。然后，为了确保我们以后可以使用匹配的结果，需要用括号将它括起来，创建一个捕获组（capture group）。接下来是一个空格符，一个等号，又一个空格符和一个 # 号。然后，我们需要匹配 6 个十六进制数字。\\p{Hex_Digit} 意思是匹配一个十六进制数字（Hex_Digit 是一个 unicode 属性名）。修饰符 {6} 意味着我们需要匹配 6 个，然后和之前一样，把这些一起用括号括起来，这样就创建了第二个捕获组

#### 扫描器（Scanner）
