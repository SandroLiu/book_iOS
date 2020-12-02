![](/assets/Snip20201202_27.png)# 新版iOS适配

## iOS 13
- 修改`UIView`的`frame`属性会调用`- layoutSubviews`方法
- `UITabbar` 设置选中颜色没有效果，显示的是蓝色，通过添加以下代码修改，之前代码不用变，只添加  


```objc
  if(@available(iOS 13.0, * )) {
      // color填未选中的颜色即可
      [tabBar setUnselectedItemTintColor:[UIColor whiteColor]];
  }
```

## xcode 12

#### 模拟器架构缺失

> NMSample's architectures (arm64) include none that iPhone 12 Pro Max can execute (Intel 64-bit).

- 添加处理器架构

```
BuildSetting -> VALID_ARCHS 添加x86_64
```
#### 使用自己的SDK，模拟器运行提示缺少ARM64架构

![](/assets/Snip20201202_27.png)