# OC与JS交互

## JavaScriptCore 实现 OC与JS交互
- JSContext JS运行环境，类似于JS中的window
    - 执行JS代码
``` objc
JSContext *context = [[JSContext alloc] init];
[context evaluateScript:@"var num = 5 + 5"];
[context evaluateScript:@"var names = ['Grace', 'Ada', 'Margaret']"];
[context evaluateScript:@"var triple = function(value) { return value * 3 }"];
JSValue *tripleNum = [context evaluateScript:@"triple(num)"];
```

- JSValue 任何出自JSContext的值都被包裹在一个JSValue对象中，包括字符串、数字、数组、对象和方法等。

### OC调用JS
- 下标值

```objc
JSValue *names = context[@"names"];
JSValue *initialName = names[0];
NSLog(@"The first name: %@", [initialName toString]);
```

- 调用方法

```objc
JSValue *tripleFunction = context[@"triple"];
JSValue *result = [tripleFunction callWithArguments:@[@5] ];
NSLog(@"Five tripled: %d", [result toInt32]);
```

- 错误处理

```objc
context.exceptionHandler = ^(JSContext *context, JSValue *exception) {
   NSLog(@"JS Error: %@", exception);
};

[context evaluateScript:@"function multiply(value1, value2) { return value1 * value2 "];
```
### JS调用OC
让 JSContext 访问我们的本地客户端代码的方式主要有两种：block 和 JSExport 协议

- Blocks

```objc
context[@"simplifyString"] = ^(NSString *input) {
   NSMutableString *mutableString = [input mutableCopy];
   CFStringTransform((__bridge CFMutableStringRef)mutableString, NULL, kCFStringTransformToLatin, NO);
   CFStringTransform((__bridge CFMutableStringRef)mutableString, NULL, kCFStringTransformStripCombiningMarks, NO);
   return mutableString;
};

NSLog(@"%@", [context evaluateScript:@"simplifyString('안녕하새요!')"]);
```

- JSExport
## UIWebView中OC与JS交互
1. UIWebView简单实现 OC与JS交互
2. UIWebView 通过 JavaScriptCore实现 OC与JS交互

## WKWebView中OC与JS交互
