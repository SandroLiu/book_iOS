# 三方库使用问题

## IQKeyboardManager

#### 不滚动问题

设置

```swift

    IQKeyboardManager.shared.enable = true
```

#### 点击外部不回收键盘

```swift
    IQKeyboardManager.shared.shouldResignOnTouchOutside = true
```

#### 不显示上下箭头

不显示上下箭头，可能是因为多个textfield不在同一个直接父视图里，需要将同一个父视图的类型设置为`IQPreviousNextView`

```swift
    containerView = IQPreviousNextView(frame: .zero)
```