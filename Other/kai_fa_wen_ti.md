# 开发问题

## 屏幕旋转设置

- 代码

```swift

override func viewDidAppear(_ animated: Bool) {
    super.viewDidAppear(animated)
    
    let value = UIInterfaceOrientation.landscapeRight.rawValue
    UIDevice.current.setValue(value, forKey: "orientation")
}

override var shouldAutorotate: Bool {
    return true
}

override var supportedInterfaceOrientations: UIInterfaceOrientationMask {
    return .all
}

```
- 注意
如果在Pad上也需要旋转需要再设置一项
![](/assets/1602811774696.jpg)
