# CocoaPods使用

### Podfile文件设置
- 忽略引入库的所有警告
```
inhibit_all_warnings!
```

### 三方库版本管理
- 在`podfile.lock`或`Manifest.lock`中有当前安装的三方库版本

### 创建公有库注意事项
- 先查看公有库名字有没有重复

### 本地校验报错 `pod podspec file not found with <angled>`
    
 本地校验出现三方库引用错误，找不到文件，是因为三方库引用有问题，例如引用`AFNetworking`，正确引用`<AFNetworking/AFNetworking.h>`，错误引用`<AFNetworking.h>`
 
### [!] Oh no, an error occurred
- 执行 pod install 时报错
- 在Error下面有错误原因
![](/assets/Snip20190123_2.png)

### target overrides the `ALWAYS_EMBED_SWIFT_STANDARD_LIBRARIES`

![](/assets/Snip20200319_1.png)

- 解决办法
![](/assets/Snip20200319_4.png)